# InstaLock

നിങ്ങളുടെ ഫോണിലെ Instagram ആപ്പ് തുറക്കുമ്പോൾ fingerprint / PIN / pattern ചോദിക്കുന്ന ഒരു ലളിതമായ Android app lock (Kotlin).

## എങ്ങനെ പ്രവർത്തിക്കുന്നു
- `LockService` (AccessibilityService) ഏത് ആപ്പാണ് മുന്നിൽ വന്നത് എന്ന് മാത്രം നോക്കുന്നു (`com.instagram.android`).
- Instagram വന്നാൽ `LockActivity` മുകളിൽ കാണിക്കുന്നു; ഫോണിന്റെ സ്വന്തം biometric/screen-lock ഉപയോഗിച്ച് അൺലോക്ക് ചെയ്യണം.
- Instagram വിട്ട് മറ്റൊരു ആപ്പിലേക്ക് പോയാൽ അടുത്ത തവണ വീണ്ടും ലോക്ക് ചോദിക്കും.
- സ്ക്രീനിലെ ഉള്ളടക്കം വായിക്കുന്നില്ല, ഇന്റർനെറ്റ് permission ഇല്ല.

## Build ചെയ്യാൻ
**Android Studio:** ഈ ഫോൾഡർ Open ചെയ്യുക → Gradle sync → Run.

**GitHub Actions:** repo-യിലേക്ക് push ചെയ്താൽ `.github/workflows/build.yml` debug APK ഉണ്ടാക്കും
(Actions → Build APK → Artifacts-ൽ നിന്ന് ഡൗൺലോഡ് ചെയ്യാം).

## ഉപയോഗിക്കാൻ
1. APK install ചെയ്ത് InstaLock തുറക്കുക.
2. "Accessibility settings തുറക്കുക" → InstaLock ഓൺ ചെയ്യുക.
3. ഫോണിൽ screen lock സെറ്റ് ചെയ്തിരിക്കണം (minSdk 30 / Android 11+).

## പരിമിതികൾ
- Accessibility service ഓഫാക്കിയാൽ ലോക്ക് പ്രവർത്തിക്കില്ല.
- ചില ഫോണുകളിൽ (Xiaomi, Oppo, Vivo...) battery optimization InstaLock-നെ നിർത്താം; ആപ്പിന് "No restrictions" കൊടുക്കുക.
- ഇത് സ്വന്തം ഫോണിലെ privacy-ക്ക് വേണ്ടിയുള്ളതാണ്, ശക്തമായ security ഉറപ്പല്ല.

## GitHub-ൽ ഇടാൻ
```bash
cd InstaLock
git init
git add .
git commit -m "Initial commit: InstaLock"
git branch -M main
git remote add origin https://github.com/<username>/InstaLock.git
git push -u origin main
```
