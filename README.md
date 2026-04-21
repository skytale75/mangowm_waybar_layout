# mangowm_waybar_layout
A waybar module to show the current mango layout
## Step One - Bash script: current_layout.sh

You need to add your monitor output name to "monitor" in the
script below. I call the file current_layout.sh

```
#!/usr/bin/env bash

monitor="HDMI-A-1"
output=$(mmsg -g -l | grep "$monitor" | awk '{print $NF}')

case "$output" in
    "T")   class="tile"              SEND="Tile"     ;;
    "S")   class="scroller"          SEND="Scroller" ;;
    "M")   class="monocle"           SEND="Monocle"  ;;
    "G")   class="grid"              SEND="Grid"     ;;
    "K")   class="deck"              SEND="Deck"     ;;
    "CT")  class="center_tile"       SEND="C Tile"   ;;
    "VT")  class="vertical_tile"     SEND="V Tile"   ;;
    "RT")  class="right_tile"        SEND="R Tile"   ;;
    "VS")  class="vertical_scroller" SEND="V Scroll" ;;
    "VG")  class="vertical_grid"     SEND="V Grid"   ;;
    "VK")  class="vertical_deck"     SEND="V Deck"   ;;
    "TG")  class="tgmix"             SEND="TGmix"    ;;
    *)     class="default"           SEND="default"  ;;
esac

echo "{\"text\": \"$SEND\", \"class\": \"$class\"}"
pkill -RTMIN+11 waybar

```

## Step Two - Add the dropdown menu xml: LayoutMenu.xml

I like to keep a waybar directory in my mango config directory, which is where I keep
my mango config files and anything that goes along with it. I put the LayoutMenu.xml file and the current_layout.sh file to the directory.

```LayoutMenu.xml
<?xml version="1.0" encoding="UTF-8"?>
<interface>
    <object class="GtkMenu" id="menu">
        <child>
            <object class="GtkMenuItem" id="tile">
                <property name="label">Tile</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="scroller">
                <property name="label">Scroller</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="monocle">
                <property name="label">Monocle</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="grid">
                <property name="label">Grid</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="deck">
                <property name="label">Deck</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="center_tile">
                <property name="label">Center Tile</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="vertical_tile">
                <property name="label">Vertical Tile</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="right_tile">
                <property name="label">Right Tile</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="vertical_scroller">
                <property name="label">Vertical Scroller</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="vertical_grid">
                <property name="label">Vertical Grid</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="vertical_deck">
                <property name="label">Vertical Deck</property>
            </object>
        </child>
        <child>
            <object class="GtkMenuItem" id="tgmix">
                <property name="label">TGmix</property>
            </object>
        </child>
    </object>
</interface>

```

## Step Three - Add the custom module to the mangowm .json file. 

You need to change the paths to the appropriate path for your system.  

```Add to waybar .json
	"custom/current_layout": {
		"exec": "~/.config/mango/waybar/current_layout.sh",
		"return-type": "json",
		"format": "{text}",
		"tooltip": false,
		"menu": "on-click",
		"menu-file": "~/.config/mango/waybar/LayoutMenu.xml",
		"menu-actions": {
			"tile": "mmsg -l T",
			"scroller": "mmsg -l S",
			"monocle": "mmsg -l M",
			"grid": "mmsg -l G",
			"deck": "mmsg -l K",
			"center_tile": "mmsg -l CT",
			"vertical_tile": "mmsg -l VT",
			"vertical_scroller": "mmsg -l VS",
			"right_tile": "mmsg -l RT",
			"vertical_grid": "mmsg -l VG",
			"vertical_deck": "mmsg -l VK",
			"tgmix": "mmsg -l TG"
		},
		"interval": 1
	}

```

## Step Four - style.css

Sdd this to your style.css file. Play with the settings and colors as you see fit.

```Add to style.css
#custom-current_layout {
  min-width: 60px;
  font-weight: bold;
  padding: 0px 10px;
  border-radius: 90px 0px 0px 90px;
  margin-left: 0px;
}

#custom-current_layout.tile {
  background-color: #60ff60;
  color: black;
}

#custom-current_layout.scroller {
  background-color: teal;
  color: black;
}

#custom-current_layout.monocle {
  background-color: #44df5a;
  color: black;
}

#custom-current_layout.grid {
  background-color: #feed4d;
  color: black;
}

#custom-current_layout.deck {
  background-color: #44df5a;
  color: black;
}

#custom-current_layout.center_tile {
  background-color: #ff567f;
  color: black;
}

#custom-current_layout.vertical_tile {
  background-color: #feed4d;
  color: black;
}

#custom-current_layout.right_tile {
  background-color: #ff567f;
  color: black;
}

#custom-current_layout.vertical_scroller {
  background-color: #51affe;
  color: black;
}

#custom-current_layout.vertical_grid {
  background-color: #feed4d;
  color: black;
}

#custom-current_layout.vertical_deck {
  background-color: #885bff;
  color: black;
}

#custom-current_layout.tgmix {
  background-color: #feed4d;
  color: black;
}


```


