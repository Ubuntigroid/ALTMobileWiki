# Установка ALT Mobile на Chuwi Hi8 Pro

Данная инструкция описывает процесс установки ОС Альт, в частности, ALT Mobile, на планшет Chuwi Hi8 Pro.

:::danger Внимание!
Все действия, описанные в данной статье, вы выполняете на свой страх и риск. Автор статьи и сообщество ALT Linux Team, а также ООО "Базальт СПО" не несут ответственность за "окирпиченные" и сгоревшие приставки, затёртые данные пользователя, а также сгоревшие инструменты и прочие последствия.
:::

### Технические характеристики

|     Компонент      |                                                 Название                                                 |         Статус         |
| :----------------: | :------------------------------------------------------------------------------------------------------: | :--------------------: |
|     Процессор      |                                 Intel®️ Atom™️  Z8300, 4ядра на 1,44 Ггц                                  |     :green_circle:     |
|      Дисплей       |                         8 дюймов, 1200x1920 пикселей, встроенная графика Intel HD                        |     :green_circle:     |
| Оперативная память |                                                DDR3L 2GB                                                 |     :green_circle:     |
| Постоянная память  |                                    32GB eMMC, слот microSD (до 64GB)                                     |     :green_circle:     |
|  Сенсорная панель  |                                         Chipone, 10 точек касания                                        |     :green_circle:     |
|        Звук        |                                             Realtek RT5651                                               |     :green_circle:     |
|      Питание       |                                          	Аккумулятор, 4 000 мА·ч                                       |     :green_circle:     |
|        WiFi        |                   Адаптер беспроводной сети Broadcom BCM43430 802.11 b/g/n 2.4GHz SDIO                   |     :green_circle:     |
|     Bluetooth      |                                            Realtek RGN RTL8723BS                                         |      :red_circle:      |
|       Камеры       |                      2MP (фронтальная) и 2MP (основная), обе на базе датчика OV2680                      |    :red_circle:(\*)    |
|  Датчик освещения  |                                             Solteam JSA-1212                                             |      :red_circle:      |
|      Гироскоп      |                                               Bosch BMG160                                               |     :green_circle:     |
|    Акселерометр    |                                           AK09911C8KXCJK-1013                                            |     :green_circle:     |
|    Вывод звука     |                                  Моно динамик, порт для наушников 3,5мм                                  |  :green_circle:(\*\*)  |
|    Вывод видео     |                                                Mini HDMI                                                 |     :green_circle:     |
|        USB         |                           Порт micro USB 2.0 (также для зарядки), порт USB 2.0                           |     :green_circle:     |

:::details Условные обозначения

:green_circle: `Работает` - работает в полном объёме

:yellow_circle: `Частично` - работает частично

:red_circle: `Не работает` - не работает

:white_circle: `Отсутствует` - не предусмотрено спецификацией

:::

### Примечания:

\* Отсутствует полноценный модуль ядра и драйвер.

\*\* Конфигурация звукового устройства не совпадает с распиновкой гнезда для наушников.

## Подготовка

Для установки ОС alt Mobile на планшет Chuwi Hi8 Pro нам понадобятся

1. Флешка или карта памяти с записанным образом ALT Reqular для x86_64

2. USB-разветвитель для клавиатуры, либо клавиатура со встроенным тачпадом

3. USB сетевая карта или WiFi-свисток

### Подготовка накопителя

1. Скачиваем образы ОС ALT Regular (для примера - IceWM)

```shell
wget http://nightly.altlinux.org/sisyphus/tested/regular-icewm-latest-x86_64.iso
```

2. Вставляем флешку / карту памяти в ПК и записываем образ regular-icewm-latest-x86_64.iso через ALT Media Writer

3. Отмонтируем флешку.

### Установка

1. Подключаем USB-разветвитель в USB-разъём, к нему - клавиатуру, мышь, сетевую карту/WiFi-свисток и флешку/вставляем карту памяти в слот.

2. Включаем планшет (зажимаем кнопку включения на 2-3 секунды), и жмём на клавиатуре клавишу Esc, пока не окажемся в BIOS.

3. Во вкладке Boot, в пункте Boot Option #1, выбираем нашу флешку/карту памяти.

4. Переходим во вкладку Save & Exit (клавиша вправо), выбираем пункт Save Changes and Exit, соглашаемся, выбрав пункт Yes и нажав на Enter, перезагружаем планшет.

5. Загружаемся в нашу ОС и открываем терминал нажатием комбинации клавиш Ctrl+Alt+T.

6. Cкачиваем образ ALT Mobile

```shell
wget http://beta.altlinux.org/mobile/sisyphus/latest/alt-mobile-phosh-un-def-20240926-x86_64.img.xz
```

7. Переходим в режим рута и переходим в домашний каталог:

```shell
[user@comp~]$ su -

[root@comp~]# cd /home/altlinux/
```

8. Узнаём название устройства eMMC и записываем образ:

```shell
lsblk

xzcat alt-mobile-phosh-un-def-<release_date>-x86_64.img.xz | dd of=/dev/<имя_eMMC> oflag=direct,sync iflag=fullblock bs=1M status=progress
```

9. По окончании процесса записи набираем в терминале команду poweroff. Планшет выключится.
После выключения вынимаем установочный накопитель.

## Доведение до ума

1. Включаем планшет и загружаемся в ОС. Первый запуск будет долгий - раздел с системой расширится на весь объём eMMC

2. Подключаемся к сети и запускаем Центр Приложений, заходим во вкладку Обновления и жмём кнопку "Обновить"

3. Устанавливаем все обновления - соглашаемся на перезагрузку. После перезагрузки планшет снова загрузится в ОС.

4. После установки обновлений нужно поставить несколько пакетов. Запускаем терминал и от рута устанавливаем следующие пакеты:

```shell
[user@comp~]$ su -

[root@comp~]# apt-get install firmware-alsa-sof settings-alsa-sof-force
```

5. Cкачиваем файл прошивки сенсорной панели по ссылке с поста на 4PDA (необходима регистрация):

```shell
https://4pda.to/forum/index.php?showtopic=703165&view=findpost&p=108025408
```

6. Создаём каталог для прошивки и копируем её с нужным именем

```shell
[root@comp~]# mkdir /lib/firmware/chipone && cp icn8505-HAMP0001.fw /lib/firmware/chipone/
```

7. Скачиваем файл прошивки и настроек для модуля WiFi:

```shell
wget https://raw.githubusercontent.com/armbian/firmware/refs/heads/master/brcm/brcmfmac43430-sdio.txt

wget https://github.com/armbian/firmware/raw/refs/heads/master/brcm/brcmfmac43430-sdio.bin
```

И копируем в каталог /lib/firmware/brcm/

```shell
cp brcmfmac43430* /lib/firmware/brcm/
```

9. Перезагружаем планшет командой reboot и (скорее всего) радуемся работающему планшету
