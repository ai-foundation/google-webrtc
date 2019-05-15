**WebRTC is a free, open software project** that provides browsers and mobile
applications with Real-Time Communications (RTC) capabilities via simple APIs.
The WebRTC components have been optimized to best serve this purpose.

**Our mission:** To enable rich, high-quality RTC applications to be
developed for the browser, mobile platforms, and IoT devices, and allow them
all to communicate via a common set of protocols.

The WebRTC initiative is a project supported by Google, Mozilla and Opera,
amongst others.

### Development

See http://www.webrtc.org/native-code/development for instructions on how to get
started developing with the native code.

[Authoritative list](native-api.md) of directories that contain the
native API header files.

### More info

 * Official web site: http://www.webrtc.org
 * Master source code repo: https://webrtc.googlesource.com/src
 * Samples and reference apps: https://github.com/webrtc
 * Mailing list: http://groups.google.com/group/discuss-webrtc
 * Continuous build: http://build.chromium.org/p/client.webrtc
 * [Coding style guide](style-guide.md)
 * [Code of conduct](CODE_OF_CONDUCT.md)

# Quick Start

#### Installing Chromium depot tools

Add this to your .bashrc
```bash
# Change to wherever you want it installed
export CHROMIUM_DEPOT_TOOLS_INSTALL_PATH=~/Workspace/chromium_depot_tools

# The chrome depot tools complain if PATH contains a literal '~'
export PATH=${PATH/\~/\$HOME}:$CHROMIUM_DEPOT_TOOLS_INSTALL_PATH

function install_chromium_depot_tools() {
    if [[ -e $CHROMIUM_DEPOT_TOOLS_INSTALL_PATH ]]; then
        echo "Already installed at $CHROMIUM_DEPOT_TOOLS_INSTALL_PATH. See environmental variable \$CHROMIUM_DEPOT_TOOLS_INSTALL_PATH."
        return 0
    fi

    git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git "$CHROMIUM_DEPOT_TOOLS_INSTALL_PATH"
}

function update_chromium_depot_tools() {
    if [[ ! -e $CHROMIUM_DEPOT_TOOLS_INSTALL_PATH ]]; then
        echo "Tools are not installed at $CHROMIUM_DEPOT_TOOLS_INSTALL_PATH. See environmental variable \$CHROMIUM_DEPOT_TOOLS_INSTALL_PATH."
        return 1
    fi

    cd "$CHROMIUM_DEPOT_TOOLS_INSTALL_PATH"
    git pull
    cd -
}
```

Load the new funcations into your session or restart your shell session
```bash
source ~/.bashrc
```

Install the tools
```bash
install_chromium_depot_tools
```

#### Set up the project

```bash
# Get the code
cd ~/Workspace
mkdir google-webrtc
cd google-webrtc
gclient root
gclient config --unmanaged --name=src --deps-file=DEPS git@github.com:ai-foundation/google-webrtc.git
gclient sync --nohooks --with_branch_heads # This can take quite a while

# Generate the Xcode project files
cd src
gn gen out/ios_xcode --args='target_os="ios" target_cpu="arm64"' --ide=xcode
open -a Xcode.app out/ios/all.xcworkspace
```


