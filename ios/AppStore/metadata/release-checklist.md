# App Store 发布清单

## 已在仓库中准备

- Xcode 工程：`ios/GuitarFred.xcodeproj`
- Bundle ID：`com.dannymaxhusky.guitarfred`
- 版本号：`1.0`
- Build：`1`
- App icon asset catalog：`ios/GuitarFred/Assets.xcassets/AppIcon.appiconset`
- App Store 1024 icon：`ios/GuitarFred/Assets.xcassets/AppIcon.appiconset/AppIcon-1024.png`
- App Store 截图：
  - iPhone 6.9：`ios/AppStore/screenshots/iphone-6.9/`
  - iPad 13：`ios/AppStore/screenshots/ipad-13/`
- 隐私清单：`ios/GuitarFred/PrivacyInfo.xcprivacy`
- 简体中文商店文案：`ios/AppStore/metadata/zh-Hans.md`

## App Store Connect 手动步骤

1. 打开 App Store Connect，创建新 App。
2. Bundle ID 选择或创建 `com.dannymaxhusky.guitarfred`。
3. SKU 建议填写 `guitarfred-ios-1`。
4. 价格选择 Paid App，并设置为 USD 9.99 对应价格点。
5. 如果账号还没启用付费 App，先由 Account Holder 接受 Paid Apps Agreement。
6. 上传 `ios/AppStore/screenshots/iphone-6.9/` 和 `ios/AppStore/screenshots/ipad-13/` 中的截图。
7. 复制 `zh-Hans.md` 中的名称、副标题、推广文本、描述、关键词和审核备注。
8. 在 Xcode 打开 `ios/GuitarFred.xcodeproj`，确认 Signing & Capabilities 的 Team 是你的 Apple Developer Team。
9. 选择 Any iOS Device，执行 Product > Archive。
10. 在 Organizer 里 Distribute App > App Store Connect > Upload。
11. 回到 App Store Connect，选择上传后的 build，补齐年龄分级、隐私问卷、版权和支持 URL 后提交审核。

## 本地验证命令

```bash
xcodebuild -project ios/GuitarFred.xcodeproj \
  -scheme GuitarFred \
  -destination 'generic/platform=iOS Simulator' \
  -configuration Debug \
  CODE_SIGNING_ALLOWED=NO \
  build
```

## 注意事项

- App Store 售价不能写进 Xcode 工程文件，只能在 App Store Connect 的 Pricing and Availability 中配置。
- App Store 上传需要 Apple Distribution 证书、有效 provisioning profile、App Store Connect 登录状态和付费协议状态；这些需要在你的 Apple Developer 账号里完成。
- 当前工程的 iPhone 方向为竖屏，iPad 方向为横屏，匹配现有产品设计。
