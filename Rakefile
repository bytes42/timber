# Provided are some Ruby snippets for easing the test, build and deploy 
# of the Timber theme

task :parse_haml do
    print "Parsing HAML layouts...\n"
    system(%{
        for f in *.haml; do [ -e $f ] && haml $f ${f%.haml}.html; done
        cd _layouts/ && 
        for f in *.haml; do [ -e $f ] && haml $f ${f%.haml}.html; done
    })
end

task :parse_sass do
    print "Parsing SASS rules...\n"
    system(%{
        cd css/ &&
        for f in *.sass; do [ -e $f ] && sass --style expanded $f ${f%.sass}.css; done
    })
end

desc "Launch preview environment"
task :preview do
    Rake::Task["parse_haml"].invoke
    Rake::Task["parse_sass"].invoke
    system "jekyll --no-safe --auto --server"
end

desc "Build site"
task :build do
    Rake::Task["parse_haml"].invoke
    Rake::Task["parse_sass"].invoke
    system "jekyll --no-safe --no-auto --no-server"
end

desc "Deploy site to 'generated' branch"
task :deploy, :src, :dest do |t, args|
  args.with_defaults(:src => "master", :dest => "gh-pages")

    # get the current branch
    currbranch = `git branch | grep ^* | cut -d' ' -f2`.chomp

    # we should only deploy from master branch
    if currbranch == args.src then

        # build site to ensure up-to-date version is deployed
        Rake::Task["build"].invoke

        # move to repo root dir
        FileUtils.cd(`git rev-parse --show-toplevel`.chomp) do

            # directory holding the generated site -- should be outside this repo
            site = `mktemp -d /tmp/_site.XXXXXXXXX`.chomp

            # copy the site
            FileUtils.cp_r "_site/.", site

            # checkout branch on which site will be deployed and 
            # commit generated site; switch back to source branch
            # afterwards
            system(%{
                git checkout #{args.dest}   ;
                cp -rf #{site}/* .          ;
                git add -v .                ;
                git commit -a -m "updated site #{Time.new.inspect}" ;
                rm -rf #{site}              ;
                git checkout #{args.src}
            })
        end
    end
end
