# USBDeviceActions.spoon

A [Hammerspoon](http://www.hammerspoon.org) Spoon that opens/closes apps or runs an arbitrary function when a USB device is connected/disconnected.

Example configuration (using [SpoonInstall.spoon](http://www.hammerspoon.org/Spoons/SpoonInstall.html)):
```lua
function toggleKeyboardLayout(x)
  if x then
    hs.keycodes.setLayout("U.S.")
  else
    hs.keycodes.setLayout("Colemak")
  end
end

spoonInstall:andUse(
  "USBDeviceActions",
  {
    config = {
      devices = {
        ScanSnapiX500EE            = { apps = { "ScanSnap Manager Evernote Edition" } },
        Planck                     = { fn = toggleKeyboardLayout },
        ["Corne Keyboard (crkbd)"] = { fn = toggleKeyboardLayout }
      }
    },
    start = true
  }
)
```

The keys of `devices` should correspond to `productName`s of USB devices. You can find the `productName` for a connected USB device using `hs.usb.attachedDevices()`).

The value of the `apps` key should contain a list of apps that will be launched/killed when the USB device is connected/disconnected. The value of the `fn` key should be a single parameter function that will be passed `true`/`false` when the USB device is connected/disconnected.
