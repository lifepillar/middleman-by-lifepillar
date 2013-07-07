# -*- coding: utf-8 -*-
require 'rubygems' if RUBY_VERSION < "1.9"
require 'pathname'

PWD = Pathname.new(__FILE__).realpath.dirname
LIB =             PWD + 'lib'
FONT_AWESOME =    LIB + 'font-awesome'
ZURB_FOUNDATION = LIB + 'zurb-foundation'
FONTS =           PWD + 'source/fonts'
JAVASCRIPTS =     PWD + 'source/javascripts'
CSS =             PWD + 'source/stylesheets'

LIB.mkpath # Make sure the lib folder exists

class Tty
  class <<self
    def blue;   bold      34; end
    def white;  bold      39; end
    def red;    underline 31; end
    def yellow; bold      33; end
    def purple; bold      35; end
    def reset;  escape     0; end
    def em;     underline 39; end
    def green;  color     92; end

  private
    def color n
      escape "0;#{n}"
    end
    def bold n
      escape "1;#{n}"
    end
    def underline n
      escape "4;#{n}"
    end
    def escape n
      "\033[#{n}m" if $stdout.tty?
    end
  end
end

# Prints a message.
def msg title, *sput
  puts "#{Tty.green}==>#{Tty.white} #{title}#{Tty.reset}"
  puts sput unless sput.empty?
end

# Print a warning message.
def owarn warning
  puts "#{Tty.red}Warning#{Tty.reset}: #{warning}"
end

# Prints an error message.
def ofail error, *info
  puts "#{Tty.red}Error#{Tty.reset}: #{error}"
  puts info unless info.empty?
end

# Prints an error message and exits.
def odie error
  ofail error
  exit 1
end


desc 'Run bundle update.'
task :bundle_update do
  sh 'bundle update'
end

desc 'Install/update Font Awesome.'
task :font_awesome do
  begin
    msg 'Downloading Font Awesome'
    sh "curl http://fortawesome.github.io/Font-Awesome/assets/font-awesome.zip -o '#{LIB}/font-awesome.zip'", :verbose => false
    msg 'Font Awesome downloaded'
    sh "rm -fr '#{LIB}/font-awesome'", :verbose => false
    msg 'Remove old copy'
    sh "unzip -d '#{LIB}' '#{LIB}/font-awesome.zip' >/dev/null", :verbose => false
    sh "rm '#{LIB}/font-awesome.zip'", :verbose => false
    msg 'Archive unzipped'

    cp Pathname.glob(LIB+'font-awesome/font/*'), FONTS, :verbose => false
    msg 'Font files copied'
    font_awesome_css = CSS+'font-awesome'
    font_awesome_css.mkpath
    sh "rsync -az --delete '#{LIB}/font-awesome/scss/' #{font_awesome_css}/", :verbose => false
    msg 'SCSS files copied'
    mv font_awesome_css + 'font-awesome.scss', font_awesome_css + '_font-awesome.scss', :verbose => false  
    mv font_awesome_css + 'font-awesome-ie7.scss', font_awesome_css + '_font-awesome-ie7.scss', :verbose => false
    msg 'font-awesome[-ie7].scss renamed'
    sh "sed -i '' -e 's/\\.\\.\\/font/..\\/fonts/' #{font_awesome_css+'_variables.scss'}", :verbose => false
    msg 'Font path fixed'
  rescue => e
    odie e
  end
  msg 'Font Awesome updated'
end

desc 'Install/update Zurb Foundation (see http://foundation.zurb.com/docs/sass.html).'
task :zurb_foundation do
  begin
    sh "bundle exec compass create '#{ZURB_FOUNDATION}' --force -r zurb-foundation --using foundation"
    zurb_js = JAVASCRIPTS
    zurb_css = CSS+'zurb-foundation'
    zurb_js.mkpath
    zurb_css.mkpath
    sh "rsync -az --delete '#{ZURB_FOUNDATION}/javascripts/foundation/' #{zurb_js}/foundation/", :verbose => false
    sh "rsync -az --delete '#{ZURB_FOUNDATION}/javascripts/vendor/' #{zurb_js}/vendor/", :verbose => false
    #cp_r Pathname.glob(ZURB_FOUNDATION+'javascripts/*'), zurb_js, :verbose => false
    msg 'Javascript files copied'
    sh "rsync -az --delete '#{ZURB_FOUNDATION}/sass/' #{zurb_css}/", :verbose => false
    #cp_r Pathname.glob(ZURB_FOUNDATION+'sass/*'), zurb_css, :verbose => false
    msg 'SCSS files copied'
    mv zurb_css + 'app.scss', zurb_css + '_app.scss', :verbose => false
    msg 'app.scss renamed'
    # Generate foundation.js.coffee
    File.open(JAVASCRIPTS+'foundation.js.coffee', 'w') do |f|
      f.puts "#= require \"foundation/foundation.js\""
      Pathname.glob("#{zurb_js}/foundation/*.*.js").each do |js|
        f.puts "#= require \"foundation/#{js.basename}\""
      end
    end
    msg 'foundation.js.coffee created'
  rescue => e
    odie e
  end
  msg 'Zurb Foundation updated'
end

desc 'Update all the components.'
task :update => [:bundle_update, :zurb_foundation, :font_awesome] do
end

#desc 'Apply patches to external components.'
#task :patch do  
#end
