# .config
Para instalar polybar :

apt install polybar

en nuestro debian,por defecto la configuración se encuentra en "~/.config/polybar/config.ini".

nano $HOME/.config/polybar/launch.sh y meter esto:
------------------------------------------------------------------------------------
#!/usr/bin/env bash

# Terminate already running bar instances
# If all your bars have ipc enabled, you can use 
polybar-msg cmd quit
# Otherwise you can use the nuclear option:
# killall -q polybar

# Launch bar1 and bar2
echo "---" | tee -a /tmp/polybar1.log /tmp/polybar2.log
polybar bar1 2>&1 | tee -a /tmp/polybar1.log & disown
polybar bar2 2>&1 | tee -a /tmp/polybar2.log & disown

echo "Bars launched..."

------------------------------------------------------------------------------------
chmod +x $HOME/.config/polybar/launch.sh

si usas i3wm, ponemos esto en "/.config/i3/config".
------------------------------------------------------------------------------------
exec_always --no-startup-id $HOME/.config/polybar/launch.sh

Y QUITAMOS el bar
------------------------------------------------------------------------------------

¡bspwm!(en bspwmrc)
------------------------------------------------------------------------------------
$HOME/.config/polybar/launch.sh
------------------------------------------------------------------------------------



luego..
nano /.config/polybar/config.ini y donde pone "bar/bar", lo dejamos en "bar/bar1".


ahora instalamos el tema de polybar 

git clone https://github.com/adi1090x/polybar-themes.git
cd polybar-themes
chmod +x setup.sh
./setup.sh o ./launch.sh
bash ~/.config/polybar/launch.sh –theme

para tenerlo automático en i3,ponemos esto en "/.config/i3/config":
exec_always --no-startup-id $HOME/.config/polybar/launch.sh --shapes
