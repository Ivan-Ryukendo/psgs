# Stack notes: mobile (Expo and React Native; most items apply to any native app)

Copy into SECURITY.md when the project ships a mobile app.

- **Anything in the bundle is public.** `EXPO_PUBLIC_*` values and everything else in the JS bundle can be extracted. No secret keys.
- **Tokens:** `expo-secure-store` (Keychain or Keystore), never AsyncStorage or plain files.
- **Transport:** HTTPS only. Android has no cleartext traffic; iOS App Transport Security has no broad exceptions.
- **Deep links and universal links:** validate every parameter. Nothing that pays, changes the account or deletes runs without login and confirmation.
- **WebViews:** restrict `originWhitelist` to your domains, and expose only the minimum through the JS bridge.
- **Permissions:** request at the moment of use, with a reason string. Remove unused ones from the app config.
- **Account deletion inside the app** if accounts can be created (App Store and Google Play require it).
- **Release build:** no dev menu, test screens, verbose logs or test endpoints. Push notifications carry no codes or private data.
- **Over-the-air updates:** only from your own project and channel. Enable code signing for updates if the platform supports it.
- **Forced update:** a minimum-version check, so a security fix can be required (H18).
- **Store forms:** the privacy labels and data-safety form match what the app collects (H17).
