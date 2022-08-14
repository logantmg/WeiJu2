# WeiJu2 (Working In Progress)

The first scriptable xposed module, provides a new way to change the application behavior.

Powered by Lua and made with ♥


# Features

- Lua Scripting
- An easy-to-used hook api
- With a package [repository](https://github.com/ikws4/WeiJu2-Scripts)


# QA

### How to write a hook?

```lua
-- You can import any java
local Toast = import("android.widget.Toast")
local Activity = import("android.app.Activity")
local Bundle = import("android.os.Bundle")
local StringBuilder = import("java.lang.StringBuilder")

hook {
  class = Activity,
  returns = void,
  method = "onCreate",
  params = {
    Bundle
  },
  after = function(this, params)
    -- This will call the `StringBuilder(CharSequence seq)` constructor
    -- to instantiate a StringBuilder object
    local sb = StringBuilder("Hello, ")
    sb:append("WeiJu2")
  
    Toast:makeText(this, sb:toString(), Toast.LENGTH_SHORT):show()
    --              ^
    -- Note: `this` is the Activity instance
  end,
}
```


### How to modify class fields?

```lua
-- With the `import` function you can bind any java class, and access all the fields and methods that defined
-- in that class. No more `XposedHelper.setStaticObjectField(Build.class, "DEVICE", "coral")` much cleaner!
local Build = import("android.os.Build")

Build.DEVICE = "coral"
Build.PRODUCT = "coral"
Build.MODEL = "Google Pixel 4XL"
Build.BRAND = "google"
Build.MANUFACTURER = "google"
Build.VERSION.RELEASE = "13"
```


### How to import a package?

```lua
require("ikws4.system_variable").setup {
  -- configs goes here
}
```


### How to create a package?

A basic package template:

```lua
--[[ 
@metadata
  return {
    name = "my_package",
    author = "you",
    version = "1.0.0",
    description = "Describle your package"
  }
@end
--]]

local config = {
}

local M = {}

M.setup = function(opts)
  config = table.extend(config, opts or {})
end

return M
```

If you want to share your work with others, you can create a PR in [WeiJu2-Scripts](https://github.com/ikws4/WeiJu2-Scripts), after it merged everyone can use your package!


# Screenshots

<img src="https://user-images.githubusercontent.com/47056144/183251553-9dce66f7-953c-45b9-b741-0ae8e0b567af.png" />
