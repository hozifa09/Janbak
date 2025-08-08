workflows:
  build-android:
    name: Build Android APK (unsigned)
    instance_type: mac_mini
    environment:
      vars:
        FLUTTER_CHANNEL: stable
    scripts:
      - name: Install Flutter
        script: |
          git clone https://github.com/flutter/flutter.git -b $FLUTTER_CHANNEL --depth 1 $HOME/flutter
          export PATH="$HOME/flutter/bin:$PATH"
          flutter --version
      - name: Get packages
        script: |
          export PATH="$HOME/flutter/bin:$PATH"
          flutter pub get
      - name: Build APK
        script: |
          export PATH="$HOME/flutter/bin:$PATH"
          flutter build apk --release
    artifacts:
      - build/app/outputs/flutter-apk/*.apk
    publishing:
      scripts:
        - name: Save artifact
          script: |
            echo "Artifacts saved."
