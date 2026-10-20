# AgriViz Android: Crop Disease Detection and Crop Recommendation

An Android app, written in Java, that detects crop diseases from leaf photos and
recommends crops from soil and weather values. Disease detection runs on the device
with TensorFlow Lite.

## Features

- **Disease detection.** Take a photo with the camera or pick one from storage; an
  on-device TensorFlow Lite model classifies it into one of 38 plant-disease classes
  and shows the top 3 predictions above a 0.4 confidence threshold, with symptoms and
  treatment notes from `assets/data.json`.
- **Crop recommendation.** Enter N, P, K, temperature, humidity, pH, and rainfall; the
  app looks the values up in `crop_recommendation.csv`, a 2,200-row dataset covering
  22 crops, and shows the matching crop.
- **Accounts.** Sign-up, login, and email verification with Firebase Authentication;
  profile data (name, email, user type) is stored in Firebase Realtime Database.
  Passwords are handled by Firebase Auth and never written to the database.
- **Chat screen and text-to-speech** for reading results aloud.

## Code layout

```
app/src/main/java/com/App/leafdisease/
  activity/     8 screens, each extending AppCompatActivity
  adapter/      MessageRVAdapter: RecyclerView adapter with two view-holder types
  components/   Classifier (TensorFlow Lite wrapper), AppSession, ValidationLogic,
                PopupAlertWithTTS
  model/        Message, UserModel
app/src/main/assets/
  model.tflite, soil.tflite   TensorFlow Lite disease classifiers (38 labels in labels.txt)
  crop_recommendation.csv     2,200-row lookup table for crop recommendation
```

## Build

1. Open the project in Android Studio.
2. Create a Firebase project, enable Email/Password sign-in and Realtime Database,
   and download its `google-services.json` into `app/`. That file isn't in this repo
   because it holds project-specific API keys.
3. Run the `app` configuration on a device or emulator.
