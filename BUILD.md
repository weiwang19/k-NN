
# Mac OS build steps 

## update cmake 
pip install cmake==3.17.2

## install xcode 
xcode-select --install

## Homebrew update
git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core fetch --unshallow

git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-cask fetch --unshallow

## Install Openblas, gcc dependencies
brew install openblas

brew link --overwrite python@3.9

brew install gcc

brew install libomp

## Build k-NN plugin
./gradlew build 

## Build Faiss JNI lib only 
cd jni/

cmake .

make opensearchknn_faiss

## Update Faiss version 

Example: upgrade to 1.7.3 release branch

git config -f .gitmodules submodule.jni/external/faiss.branch 1.7.3_release

git submodule sync

git submodule update --init --remote
