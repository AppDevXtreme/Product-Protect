workspace 'ProductProtect'

inhibit_all_warnings!
use_frameworks!
install! 'cocoapods', :deterministic_uuids => false

def shared_all_pods
    pod 'RealmSwift'
    pod 'LogKit'
    # specific commit includes watchos 2 support
    pod 'HxColor', :git => 'https://github.com/artman/HexColor.git', :commit => 'aa0e740'
    # common framework needs to be included as a pod to have cocoapods of it's own
    pod 'AppCommon', :path => 'AppCommon/'
end

def shared_test_pods
    pod 'Nimble'
end

target 'App' do
    platform :ios, "8.2"
    shared_all_pods
    
    pod 'KFSwiftImageLoader'
    pod 'Cartography', '0.7.0'
    pod 'Fabric'
    pod 'Crashlytics'
    pod 'SwiftyTimer', '1.4.1'
    pod 'QRCodeReader.swift', :git => 'https://github.com/jamesmalcolmXDesign/QRCodeReader.swift'
    pod 'KMPlaceholderTextView', '~> 1.2.0'
    pod 'TPKeyboardAvoiding'
    #pod 'VWWPermissionKit', '1.1.2'
    pod 'VWWPermissionKit', :git => 'https://github.com/RossOliver87/VWWPermissionKit'
    pod 'ReachabilitySwift', '~> 2.4'
end

target 'AppTests' do
    platform :ios, "8.2"
    shared_test_pods
end

target 'AppCommonTests' do
    platform :ios, "8.2"
    shared_test_pods
end
