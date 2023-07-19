# Void Linux guide by YJJX

Помощь по XBPS
https://github.com/void-linux/void-packages

Руководство установки
https://docs.voidlinux.org/installation/

###### Установка xtools и nonfree & multilib для удобства
```
sudo xbps-install -Suv
sudo xbps-install xtools
xi void-repo-nonfree void-repo-multilib void-repo-multilib-nonfree
```
###### Установка KDE Plasma в чистый Void Linux
```
xi xorg kde5 kde5-baseapps dbus sddm
sudo ln -s /etc/sv/dbus /var/service
sudo ln -s /etc/sv/sddm /var/service
```
###### Опционально для Wi-Fi и Bluetooth
```
xi bluez bluez-alsa NetworkManager
sudo ln -s /etc/sv/NetworkManager /var/service
sudo ln -s /etc/sv/bluetoothd /var/service
```
###### Драйвера для nvidia
```
xi nvidia nvidia-libs nvidia-libs-32bit vulkan-loader vulkan-loader-32bit Vulkan-ValidationLayers Vulkan-ValidationLayers-32bit Vulkan-Headers Vulkan-Tools mesa-32bit mesa-dri-32bit mesa-dri
```
###### Драйвера intel
```
xi mesa-dri linux-firmware-intel intel-video-accel mesa-vulkan-intel Vulkan-ValidationLayers Vulkan-ValidationLayers-32bit Vulkan-Headers Vulkan-Tools mesa-32bit mesa-vulkan-intel-32bit  vulkan-loader vulkan-loader-32bit
```
###### Драйвера vulkan для AMD
```
xi linux-firmware-amd mesa-dri mesa-vaapi mesa-vdpau Vulkan-ValidationLayers Vulkan-ValidationLayers-32bit Vulkan-Headers Vulkan-Tools vulkan-loader vulkan-loader-32bit mesa-vulkan-radeon mesa-32bit amdvlk amdvlk-32bit mesa-vulkan-radeon mesa-vulkan-radeon-32bit
```
###### Программы
```
xi -Suv neofetch nano ffmpeg xclip kdenlive krita gimp inkscape gwenview wine wine-32bit wine-gecko wine-mono wine-devel winetricks steam lutris kcalc okular gparted libreoffice libreoffice-i18n-ru obs audacity firefox firefox-i18n-ru ark vlc qbittorrent android-tools noto-fonts-cjk noto-fonts-emoji kdegraphics-thumbnailers ffmpegthumbs ssr git curl

noto-fonts-cjk noto-fonts-emoji  -- шрифты и смайлы для браузера
xclip -- для работы с буфером обмена
kdenlive -- для редактирования видео
krita -- для создания/редактирования изображений
gimp -- для редактирования изображений
inkscape -- для создания/редактирования векторных изображений
wine & etc -- для запуска виндового софта
libreoffice -- офис
obs -- для записи видео
audacity -- для записи/редактирования аудио
spectacle -- для создания скриншотов
ark -- архиватор
vlc -- для просмотра видео
qbittorrent -- торент клиент
kdegraphics-thumbnailers ffmpegthumbs -- превью видео и pdf для dolphin
android-tools -- для управления смартфоном через Fastboot и ADB
ssr -- SimpleScreenRecorder

```
###### Установка VirtualBox в Void Linux
```
xi linux-headers base-devel virtualbox-ose
sudo modprobe vboxdrv
sudo gpasswd -a $USER vboxusers

```
*Установить VirtualBox Oracle VM VirtualBox Extension Pack
*для поддержки USB устройств в виртуальной машине
https://www.virtualbox.org/wiki/Downloads

###### Установка сторонник программ, обязательно без sudo, на примере appName
```
git clone git://github.com/void-linux/void-packages.git 
cd void-packages 
./xbps-src binary-bootstrap 
echo XBPS_ALLOW_RESTRICTED=yes >> etc/conf
./xbps-src pkg appName

# Теперь пакет нужно установить командой (через sudo)
xi --repository hostdir/binpkgs/nonfree appName
# hostdir/binpkgs -- открытые пакеты
# hostdir/binpkgs/nonfree -- закрытые пакеты

```

###### Проверить обновления программ через xbps-src
```
./void-packages/xbps-src update-check appName
```
######  Обновить приложения xbps-src
```
cd void-packages
git pull
xbps-src bootstrap-update
xi -f %package%

# или

cd void-packages
git pull
./xbps-src bootstrap-update
./xbps-src pkg %package%
xi --repository hostdir/binpkgs/nonfree %package%
```
