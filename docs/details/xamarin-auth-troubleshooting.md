# Xamarin.Auth Troubleshooting 

## Control does not return to the app after login

If you are using NativeUI (SafariViewController and [Chrome] Custom Tabs) check 

1.	schema for `redirect_url` should not be http[s] schema!

	
2.	app-linking (deep-linking) implementation 

3.	on Android there have been reports that AntiVirus software might block
	IntentFilters.
	
	Reported by 
	
```bash
	adb shell am start \
		-a android.intent.action.VIEW \
		-d "com.googleusercontent.apps.<your-android-app-id>:/oauth2redirect"
```	

## The "LinkAssemblies" task failed unexpectedly - Failed to resolve - LaunchUrl

### Problem

Linking fails for Android applications.

	The "LinkAssemblies" task failed unexpectedly.
	Mono.Linker.MarkException: 
	Error processing method: 
		'System.Void Android.Support.CustomTabs.Chromium.SharedUtilities.CustomTabActivityHelper::LaunchUrlWithCustomTabsOrFallback(Android.App.Activity,Android.Support.CustomTabs.CustomTabsIntent,Android.Net.Uri,Android.Support.CustomTabs.Chromium.SharedUtilities.ICustomTabFallback)'
		in assembly: 'Xamarin.Auth.dll' ---> 
		Mono.Cecil.ResolutionException: 
		Failed to resolve System.Void Android.Support.CustomTabs.CustomTabsIntent::LaunchUrl(Android.Content.Context,Android.Net.Uri)
		
From github


> Confirm linker issues with Xamarin.Auth 1.5.0.3 + Xamarin.Android.Support.CustomTabs 23.4.0.1:

### Analysis

TODO

### [Re]Solution/Workaround

1.	simply update Xamarin.Android.Support nuget packages to 25.0.0+ version

2.	turn off linker

Xamarin.Auth lowest pinned) versionWhen Xamarin.Forms support was added to Xamarin.Auth in 2017-05 the 
Xamarin.Android.Support libraries were pinned to 23.0.0 version in Xamarin.Forms.


## Detecting Cancellation in CustomTabs on Android

Xamarin.Auth [curerntly] cannot handle certain events in CustomTabs, because there is no
such API provided from CustomTabs. Though this issue is under investigation for possible
solutions!

References/link for similar issue:

1.	AppAuth

	https://github.com/openid/AppAuth-Android/issues/102
	\#102 Detecting user initiated closing of the authorization flow. 

	https://github.com/openid/AppAuth-Android/pull/109
	\#109 Use an intermediary activity to manage the authorization flow 
	
2.	StackOverflow

	https://stackoverflow.com/questions/41010017/callback-on-dismiss-of-chrome-custom-tabs
	
	
	