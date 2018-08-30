# XcodeGen

This is an example project to test **XcodeGen** and to present it to my colleagues. Have a look at their [GitHub][XcodeGen] Repo. There you can find every information you need!

---

### "XcodeGen is a command line tool written in Swift that generates your Xcode project using your folder structure and a project spec."

These are some of the main advantages why it could be a good idea to use XcodeGen. On their [GitHub][XcodeGen] page you can see the full list.

>- Generate projects on demand and remove your `.xcodeproj` file from git, which means **no more merge conflicts**!
>- Groups and files in Xcode are always **synced** to your directories on disk
>- Easy **configuration** of projects which is human readable and git friendly
>- Easily copy and paste **files and directories** without having to edit anything in Xcode
>- Automatically generate Schemes for **different environments** like test and production
>- Easily **create new projects** with complicated setups on demand without messing around with Xcode
>- Generate from anywhere including on **CI**

---

## Install
```
brew install xcodegen
```

## Usage
```
xcodegen
```

## Example 
`project.yml`

```yml
name: xcodegenExample # The name of the App
options: # Some general settings for the projectproject.yml
  createIntermediateGroups: true # If the folders are nested, also nest the groups in Xcode
  indentWidth: 4 # indent by 4 spaces
  tabWidth: 4 # a tab is 4 spaces
  bundleIdPrefix: "de.adorsys.ios"
configs:
  Debug: debug
  integ: debug
  test: debug
  Release: release
targets:
  xcodegenExample:
    type: application
    platform: iOS
    deploymentTarget: "11.0"
    sources:  
      - path: xcodegenExample
    scheme: 
      testTargets:
        - xcodegenExampleTests
        - xcodegenExampleUITests
      gatherCoverageData: true
  xcodegenExampleTests:
    type: bundle.unit-test
    platform: iOS
    deploymentTarget: "11.0"
    sources:
      - path: xcodegenExampleTests
    dependencies:
      - target: xcodegenExample
    scheme: 
      testTargets:
        - xcodegenExample
        - xcodegenExampleTests
      gatherCoverageData: true
  xcodegenExampleUITests:
    type: bundle.ui-testing
    platform: iOS
    sources:
      - path: xcodegenExampleUITests
    dependencies:
      - target: xcodegenExample
```

## Further information
- [XcodeGen][XcodeGen] on GitHub
- [XcodeGen-Article][Article]: Better iOS projects: Getting (nearly) rid of Xcodeproject - A (not so) short Introduction to Xcodegen ~ Number 42

[XcodeGen]: https://github.com/yonaskolb/XcodeGen
[Article]: https://www.number42.de/blog/2018/07/24/xcodegen-article.html
