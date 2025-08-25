HTML → AAP (Android App) — GitHub Builder

How to use:
1) Put your web app content in /web (at minimum, index.html). Optional: assets.zip and icon.png (512x512).
2) Commit/push to GitHub.
3) In the repo, go to Settings → Secrets and variables → Actions and add these secrets:
   - UPLOAD_ALIAS
   - UPLOAD_STOREPASS
   - UPLOAD_KEYPASS
   - UPLOAD_KEYSTORE_BASE64  (base64 of your JKS keystore)
   To create a keystore:
      keytool -genkeypair -v -keystore upload.jks -storetype JKS -keyalg RSA -keysize 4096 -sigalg SHA256withRSA -validity 9125 -alias upload
   To base64 encode (Windows PowerShell):
      [Convert]::ToBase64String([IO.File]::ReadAllBytes("upload.jks"))

4) Open the Actions tab → run “Build Signed AAB/APK from HTML”.
5) Download the 'signed-build' artifact (AAB+APK).

Defaults in workflow:
- APP_NAME = HTML → AAP Converter
- APP_ID   = com.html.aap.converter
- VERSION  = 1.0 (1)
- SDKs     = min 21, target 35
- PERMS    = INTERNET,ACCESS_NETWORK_STATE

Edit .github/workflows/build.yml to change them.
