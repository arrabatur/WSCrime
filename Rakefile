# -*- coding: utf-8 -*-
$:.unshift("/Library/RubyMotion/lib")
require 'motion/project/template/ios'
require 'bundler'
Bundler.setup
Bundler.require

Motion::Project::App.setup do |app|
  app.name = "W-S Crime"
  app.identifier = "com.mohawkapps.Winston-Salem-Crime"
  app.frameworks += %w(CoreLocation MapKit QuartzCore AVFoundation CoreGraphics StoreKit)
  app.device_family = [:iphone, :ipad]
  app.version = '12'
  app.short_version = '1.8.1'
  app.interface_orientations = [:portrait, :landscape_left, :landscape_right, :portrait_upside_down]
  app.deployment_target = "6.0"
  app.info_plist['APP_STORE_ID'] = 472546582
  app.icons = Dir.glob("resources/icon*.png").map{|icon| icon.split("/").last}

  app.vendor_project('vendor/ARKit', :xcode, :headers_dir => 'ARKitLib/ARKit')
  app.vendor_project('vendor/TimesSquare', :static, :cflags => '-fobjc-arc')

  app.pods do
    pod 'FlurrySDK'
    pod 'Appirater'
  end

  app.development do
    app.entitlements['get-task-allow'] = true
    app.codesign_certificate = "iPhone Developer: Mark Rickert (YA2VZGDX4S)"
    app.provisioning_profile = "./Provisioning/WSCMDevelop.mobileprovision"
  end

  app.release do
    app.entitlements['get-task-allow'] = false
    app.codesign_certificate = "iPhone Distribution: Mohawk Apps, LLC (DW9QQZR4ZL)"
    app.provisioning_profile = "./Provisioning/WSCMDistribute.mobileprovision"
  end

end

desc "Open latest crash log"
task :log do
  app = Motion::Project::App.config
  exec "less '#{Dir[File.join(ENV['HOME'], "/Library/Logs/DiagnosticReports/#{app.name}*")].last}'"
end
