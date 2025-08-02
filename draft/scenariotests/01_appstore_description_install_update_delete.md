**Date:** 2025‑08‑02  
**File:** 01_appstore_description_install_update_delete.md  
**Purpose:** Check that the **SelfFull** app can be found, installed, updated (manual + auto) and deleted in both the Apple App Store and Google Play Store.

---

# Test Scenario – Store Listing, Install, Update & Delete

## 0  Pre‑conditions
- Device has internet access and at least 100 MB free storage  
- iOS 15 + or Android 11 +  
- User is signed in to App Store / Play Store  
- For *Update* path: an older SelfFull version is already installed  

---

## A  Store Listing

1. **Search “SelfFull” in the store**  
   - Appears in top‑5 search results  
   - Icon, name and developer correct  

2. **Open the SelfFull store page**  
   - Title and description are present and readable  
   - At least 5 screenshots shown  
   - Version number and “Last updated” date visible  

---

## B  Installation

1. **Tap “Install” / “Get”**  
   - Download bar appears and completes without error  
2. **Open the app after install**  
   - Icon now on home screen / drawer  
   - App launches to main dashboard within ~10 s  
3. **Verify version**  
   - In‑app settings show same version as store page  

---

## C  Update

### Manual update
1. Open store page with old version installed → **Tap “Update”**  
   - App updates without error  
2. Launch SelfFull  
   - User data (login, settings) still present  
   - Version number increased  

### Automatic update (Play Store)
1. Enable **Auto‑update apps** in Play Store settings  
2. Leave device on Wi‑Fi for ≥ 30 min  
   - SelfFull updates in the background  

---

## D  Deletion

1. **Long‑press SelfFull icon → “Remove App” / “Uninstall”**  
   - Confirmation dialog shows correct name  
2. **Confirm deletion**  
   - Icon disappears; app no longer listed in settings  
3. **Optional:** Re‑install to confirm clean uninstall  

---

**End of file**