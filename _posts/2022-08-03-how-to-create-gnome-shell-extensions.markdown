---
layout: post
title:  "How to Create Gnome-Shell Extensions"
date:   2022-08-03 15:07:16 +0300
categories: linux, gnome, extension
---
In this article, we will learn simple doing gnome-shell extension for Pardus-21 Gnome desktop. We will add an icon to the top panel with this extension and it sends us a notification when clicking the icon.

Firstly, we open the home folder and show the hidden files with ‘ctrl+h’. Then we go to the directory .local/share/gnome-shell/extensions. Here we create a new folder named ‘example@example.com’ in the extensions folder. We create extension.js and metadata.json files in the example@example.com.

Metadata.json file includes information of extension. It is written as shown below :

### metadata.json

    { 
        "uuid": "example@example.com", 
        "name": "Example", 
        "description": "This extension puts an icon in the panel with a simple popup menu.", 
        "version": 1, 
        "shell-version": [ "3.38" ], 
        "url": "" 
    }
    

*   Uuid: It is a unique name and must same as the folder name.
*   Name: Extension’s name. It should be short and descriptive. For example Application Menu, Extension List, Dash to Dock.
*   Description: Shortly describes what the extension is.
*   Version: Defines the version of the extension.
*   Shell-version: The version of gnome used. Pardus 21 uses gnome version 3.38.
*   Url: Generated extension's link.

After creating the metadata.json file, we create the extension.js file.

### extension.js

    'use strict'; 
    
    const ExtensionUtils = imports.misc.extensionUtils; 
    const Me = ExtensionUtils.getCurrentExtension(); 
    
    function init() { 
        log(`initializing ${Me.metadata.name} version ${Me.metadata.version}`); 
    } 
    
    function enable() { 
        log(`enabling ${Me.metadata.name} version ${Me.metadata.version}`); 
    } 
    
    function disable() { 
        log(`disabling ${Me.metadata.name} version ${Me.metadata.version}`); 
    }
    

The skeleton version of our extension.js file is as above. Now firstly we add the libraries we will use.

    'use strict';  
    
    const {Gio, GLib, GObject, St} = imports.gi;  
    const Main = imports.ui.main; 
    const PanelMenu = imports.ui.panelMenu; 
    const PopupMenu = imports.ui.popupMenu; 
    
    const ExtensionUtils = imports.misc.extensionUtils;  
    const Me = ExtensionUtils.getCurrentExtension(); 
    
    function init() { 
        log(`initializing ${Me.metadata.name} version ${Me.metadata.version}`); 
    } 
    
    function enable() { 
        log(`enabling ${Me.metadata.name} version ${Me.metadata.version}`); 
    } 
    
    function disable() { 
        log(`disabling ${Me.metadata.name} version ${Me.metadata.version}`); 
    }
    

Now we add an icon for our extension.

    'use strict'; 
    
    const {Gio, GLib, GObject, St} = imports.gi; 
    const Main = imports.ui.main;
    const PanelMenu = imports.ui.panelMenu;
    const PopupMenu = imports.ui.popupMenu;
    
    const ExtensionUtils = imports.misc.extensionUtils; 
    const Me = ExtensionUtils.getCurrentExtension();
    
    let Indicator = GObject.registerClass(
        class Indicator extends PanelMenu.Button{
    
            _init() {
                super._init(0.0, `${Me.metadata.name} Indicator`, false);
    
                let icon =new St.Icon({
                    icon_name: 'face-smile-symbolic',
                    style_class: 'system-status-icon'
                });
                this.actor.add_child(icon);
            }        
    });
    
    let indicator = null;
    
    function init() { 
        log(`initializing ${Me.metadata.name} version ${Me.metadata.version}`); 
    } 
    
    function enable() { 
        log(`enabling ${Me.metadata.name} version ${Me.metadata.version}`);
    
        indicator = new Indicator();
        Main.panel.addToStatusArea(`${Me.metadata.name} Indicator`, indicator);
    } 
    
    function disable() { 
        log(`disabling ${Me.metadata.name} version ${Me.metadata.version}`); 
    
        if (indicator !== null) {
            indicator.destroy();
            indicator = null;
        }
    }
    

Then we create a notification adding a popup menu to our extension.

    'use strict'; 
    
    const {Gio, GLib, GObject, St} = imports.gi; 
    const Main = imports.ui.main;
    const PanelMenu = imports.ui.panelMenu;
    const PopupMenu = imports.ui.popupMenu;
    
    const ExtensionUtils = imports.misc.extensionUtils; 
    const Me = ExtensionUtils.getCurrentExtension();
    
    let Indicator = GObject.registerClass(
        class Indicator extends PanelMenu.Button{
    
            _init() {
                super._init(0.0, `${Me.metadata.name} Indicator`, false);
    
                let icon =new St.Icon({
                    icon_name: 'face-smile-symbolic',
                    style_class: 'system-status-icon'
                });
                this.actor.add_child(icon);
    
                let item = new PopupMenu.PopupMenuItem(_('Show Notification')); 
                item.connect('activate', () => {
                    Main.notify(_('Whatʼs up?'));
                });
                this.menu.addMenuItem(item);
            }        
    });
    
    let indicator = null;
    
    function init() { 
        log(`initializing ${Me.metadata.name} version ${Me.metadata.version}`); 
    } 
    
    function enable() { 
        log(`enabling ${Me.metadata.name} version ${Me.metadata.version}`);
    
        indicator = new Indicator();
        Main.panel.addToStatusArea(`${Me.metadata.name} Indicator`, indicator);
    } 
    
    function disable() { 
        log(`disabling ${Me.metadata.name} version ${Me.metadata.version}`); 
    
        if (indicator !== null) {
            indicator.destroy();
            indicator = null;
        }
    }
    

Finally, we run the r command doing ‘alt+f2’. We will see in there the name of our extension when we look at the tweaks app.

![alt text](/assets/post-gnome-shell-extensions/example.drawio.png)

Now our extension is running.

![alt text](/assets/post-gnome-shell-extensions/screenshot1.png)

* * *

The second way is;

We create a gnome-shell extension from the terminal. To do this in the terminal:

    gnome-extensions create –-interactive
    

We write and run.

Firstly, we enter the name of our extension.

![alt text](/assets/post-gnome-shell-extensions/screenshot2.png)

Then we write the description of our extension.

![alt text](/assets/post-gnome-shell-extensions/screenshot3.png)

Final, we write the uuid and we are done.

![alt text](/assets/post-gnome-shell-extensions/screenshot4.png)

Now the skeleton of our extension is ready. We write code in the extension.js file as we did above and doing alt+f2 we are running our extension.

For more information visit the [Gnome Wiki](https://wiki.gnome.org/Projects/GnomeShell/Extensions).

