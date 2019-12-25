# AppHub

functions:
- parse ipa, apk to get a verison
  - name
  - version
  - bundleid
- config admin password
- platform(ios/android) + bundleID define a app, app has many versions, app has a unique id
- update app info(icon, name) every time when we upload
- define a user version for display
  - android: versionCode define a version
  - ios: (versio + build) define a version
- each version has a download page
- each app has a download apge(always link to latest version)
- store download count
- preview could be protected by a password
- external api for ci usage
- figure out ios package tyep: ad-hoc, appstore, etc...
- get device count when ad-hoc
- upload progress
- android support multiple channel packages
- download all packages of a version in zip 

pages:
- index(login)
- app page(handle no app)
- upload
- app page: laetst version
- version page(pc + mobile): list packages
- package page(pc + mobile): specific package

we have a root data dir

model
/[id]
app:
  - id: string primary key generated, editable
  - icon: path relative to root data dir
  - name: string
  - type: 'ios' / 'android'
  - bundle id: string
  - install_password: string // empty means no password
  - download_count: int
  - created_at: ts
  - updated_at: ts

/version/[version]
version:
  - version: full generated string primary key unique
  - app_id: app id
  - androidVersionCode
  - androidVersionName
  - iosShortVersion
  - iosBundleVersion
  - created_at: ts
  - remark: string
  - download_count

/package/[package_id]
package:
  - id: string random generated primary key
  - version_id: foreign key
  - download_count
  - name: extracted from filename, editable, corresponding to filename in disk
  - size: int in bytes
  - created_at: ts
  - remark: string