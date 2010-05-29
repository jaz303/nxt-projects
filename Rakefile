require 'fileutils'

OPTS='-S=usb'

def synthesize(dir)
  
  source = dir + ".nxc"
  object = dir + ".nxb"
  
  desc("compile #{source}")
  task(dir.to_sym) do
    puts "compiling #{source}..."
    puts `cd #{dir}; nbc #{OPTS} -O=#{object} #{source}`
  end
  namespace(dir) do
    
    desc("download '#{dir}' to NXT")
    task(:download => dir.to_sym) do
      puts "downloading '#{dir}'..."
      puts `cd #{dir}; nbc #{OPTS} -b -d #{object}`
    end
    
    desc("run '#{dir}'")
    task(:run => dir.to_sym) do
      puts "running '#{dir}'..."
      puts `cd #{dir}; nbc #{OPTS} -b -d -r #{object}`
    end
    
  end
end

Dir['*'].each do |f|
  synthesize(f) if File.directory?(f)
end
