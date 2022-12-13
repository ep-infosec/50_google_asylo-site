require 'html-proofer'

task :test do
  sh "jekyll build -d /tmp/_site"
  typhoeus_configuration = {
  :timeout => 30,
#  :verbose => true
  }
  options = { :check_html => true,
              # :validation => { :report_missing_names => true, :report_invalid_tags => true },
              :enforce_https => false, # we should turn this on eventually
              :directory_index_file => "index.html",
              :check_external_hash => false,
              :assume_extension => true,
  #            :log_level => :debug,
              :url_ignore => [/localhost|github\.com\/google\/asylo-site\/edit\/master\//,
                              # Until the repos are public:
                              /github\.com\/google\/asylo.*/],
              :file_ignore => [
                # Doxygen produces objectionable HTML
                /\/doxygen\//,
                # Until crosslinks work
                /\/docs\/reference\/proto\//
              ],
              :typhoeus => typhoeus_configuration,
            }
  HTMLProofer.check_directory("/tmp/_site", options).run
end
