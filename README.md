# build-openssl-android
Build openssl library 1.1.0f on Android using NDK r15b

wget https://www.openssl.org/source/openssl-1.1.0f.tar.gz

wget https://wiki.openssl.org/images/7/70/Setenv-android.sh

mv Setenv-android.sh setenv-android.sh

dos2unix setenv-android.sh

chmod a+x setenv-android.sh

export ANDROID_NDK_ROOT=/opt/android/android-ndk-r15b

// edit setenv-android.sh:

// _ANDROID_EABI="arm-linux-androideabi-4.9"

// _ANDROID_API="android-16"

. ./setenv-android.sh

tar -xvzf openssl-1.1.0f.tar.gz 

cd openssl-1.1.0f

./config shared no-ssl2 no-ssl3 no-comp no-hw no-engine --openssldir=/usr/local/ssl/android-16/

make dep

make all

find . -name libcrypto.a

readelf -h ./libcrypto.a | grep -i 'class\|machine' | head -2

