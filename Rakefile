task 'assets:precompile' do
  require 'bundler'
  Bundler.require
  
  # Dont use digest paths
  digest = false
  public_path = './public/assets'
  bundles = %w[style.css pattern.png]
  
  root_path = File.dirname(__FILE__)
  FileUtils.rm_rf(public_path, secure: true)
  
  Sprockets::Environment.new(root_path) do |env|
    env.js_compressor = YUI::JavaScriptCompressor.new(munge: true, optimize: true)
    env.css_compressor = YUI::CssCompressor.new
    
    %w[app lib vendor].each do |path|
      %w[fonts images javascripts stylesheets].each do |asset_path|
        env.append_path(File.join(root_path, path, 'assets', asset_path))
      end
    end
    
    Sprockets::StaticCompiler.new(env, public_path, bundles, digest: digest).compile
  end
end