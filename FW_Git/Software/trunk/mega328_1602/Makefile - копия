###############################################################################
# Makefile for the project TransistorTester
###############################################################################

## General Flags
PROJECT = TransistorTester
TARGET = $(PROJECT).elf
VPATH = ..:../bitmaps
CC = avr-gcc

CPP = avr-g++

CFLAGS = -Wall

# ********************** Änderbare Flags zur Configuration des Transistortesters
# ********************** config options for your Semiconductor tester
# Every changing of this Makefile will result in new compiling the whole
# programs, if you call make or make upload.

# Select your Part-No. for avrdude :
# atmega8  : m8
# atmega168: m168 or m168p
# atmega328: m328 or m328p
# atmega1280: m1280	// see config.h for different port setting
# atmega2560: m2560	// see config.h for different port setting
PARTNO = m328p

# The WITH_MENU option enables a dialog to choose some additional functions.
# Currently a frequency measurement at ATmega Pin PD4, a frequency generator at TP2 ,
# the external voltage measurement and C+ESR measurement can be selected. Of course you can also return to
# the normal transistor tester function and switch off the tester.
#
# Активируется меню выбора функций для ATmega328.Вы сможете выбрать 
# некоторые дополнительные функции работы прибора из меню при длительном (> 0,5с)нажатии кнопки TEST.
CFLAGS += -DWITH_MENU
#
# For ATmega328 the menu function "rotary encoder check" is only enabled with the WITH_ROTARY_CHECK option.
#CFLAGS += -DWITH_ROTARY_CHECK

CFLAGS += -DWITH_FREQUENCY_DIVIDER

# With the menu item "Show data" the used icons and the font data are displayed for
# graphical displays after the presentation of calibration data.
# You can switch off the presentation of the icons and the font data by setting
# the option NO_ICONS_DEMO to save flash memory and display time.
#CFLAGS += -DNO_ICONS_DEMO

# The menu function can be easier controlled with a incremental encoder (rotary switch).
# Both switches of the rotary switch can be connected with 1 kOhm resistors to PD1 and PD3.
# The common contact of the two switches must be connected to GND.
# You must also connect both switch contacts with two 10 kOhm resistors to VCC (pull up).
# The best choise is a incremental encoder with Push Button. The button can be connected
# parallel to the start key of the Transistor Tester.
# A define of the WITH_ROTARY_SWITCH enable the support for this extension.
# If your encoder has the same count of pulses at any switch as indexed positions (detent) for every turn,
# you should set the WITH_ROTARY_SWITCH to 2 or 3.
# If your encoder has twice the count of indexed positions, you should set the WITH_ROTARY_COUNT to 1.
# For rotary encoder without indexed position or with an indexed position at every change of
# the state of any switches (four times the count of pulses) you can set the
# WITH_ROTARY_COUNT to 5 for getting the best resolution.
# You can also use two separate push-buttons for Up and Down instead ot the rotary encoder.
# You must set the WITH_ROTARY_SWITCH to 4 for the UP/DOWN push-buttons.
#
# WITH_ROTARY_SWITCH .
# Использование поворотного инкрементального энкодера в качестве опции для быстрого доступа
# в меню дополнительных функций (смотрите описание 2.5 в разделе Улучшения и расширения к прибору).
# Если количество циклов переключения контактов, за каждый оборот Вашего энкодера, соответствует количеству фиксированных позиций,
# Вы должны установить значение WITH_ROTARY_SWITCH=2 или 3.
# Если полный цикл переключения требует поворота энкодера на две фиксированные позиции, то опцию WITH_ROTARY_SWITCH нужно установить =1.
# Установка опции WITH_ROTARY_SWITCH равной 5 выбирает максимальное разрешения энкодера.
# Каждый цикл переключения в двух каналах дает 4 результата состояния счетчиков.
# Обычно этот параметр полезен только для энкодеров без фиксации. 
# Значение опции WITH_ROTARY_SWITCH равной 4 необходимо, если установлено две отдельные кнопки «Вверх» и «Вниз» вместо энкодера.
# Не используйте значение 4 если у Вас установлен энкодер!
#CFLAGS += -DWITH_ROTARY_SWITCH=2

# the option CHANGE_ROTARY_DIRECTION changes the rotary direction by swap of switches
#CFLAGS += -DCHANGE_ROTARY_DIRECTION
# The best solution for connecting the rotary switch is PD1 and PD3, because this setting can be used
# with character and ST7565 LCD. But the first draft has used PD2 instead of PD1.
# To return to the old setting, you can override the PD1 default setting with the following setting:
# CFLAGS += -DROTARY_2_PIN=PD2

# Select your language:
# Определяет выбранный язык: (Русский или украинский язык требует LCD-дисплей с кирилличе-ской кодировкой.)
# Available languages are:    LANG_BRASIL, LANG_CZECH, LANG_DANISH, LANG_DUTCH, LANG_ENGLISH, LANG_GERMAN,
# В настоящее время доступны: LANG_HUNGARIAN, LANG_ITALIAN,LANG_LITHUANIAN, LANG_POLISH, LANG_RUSSIAN,
#                             LANG_SLOVAK, LANG_SLOVENE, LANG_SPANISH, LANG_UKRAINIAN
#UI_LANGUAGE = LANG_RUSSIAN
UI_LANGUAGE = LANG_ENGLISH

# The LCD_CYRILLIC option is necessary, if you have a display with cyrillic characterset.
# This lcd-display don't have a character for Ohm and for µ (micro).
# Russian language requires a LCD controller with russian characterset and option LCD_CYRILLIC!
#
# Необходима для некоторых LCD дисплеев с кодировкой для европейских или кириллических языков.
# Символы µ и Ohm отсутствуют в их кодировке. 
# Если Вы выбрали эту опцию,то оба символа отображаются на LCD дисплее программно.
#CFLAGS += -DLCD_CYRILLIC

# The LCD_DOGM option must be set for support of the DOG-M type of LCD modules with ST7036 controller.
# For this LCD type the contrast must be set with software command.
#
# Должна быть установлена,если применяется LCD дисплей с контроллером ST7036 (тип DOG-M).
# Контрастность LCD дисплея устанавливают командами программного обеспечения.
# Если значение контраста изменено не корректно и на дисплее ничего не видно, то Вы можете попытаться его отрегулировать при просмотре дисплея под большим углом.
# Если и это не решило проблему,то надо переписать содержимое EEPROM при помощи ISP программатора.
#CFLAGS += -DLCD_DOGM

# Can be used with a 4x20 character display for better using the additional space.
# Additional parameters, which are shown only short in row 2, will be shown in row 3 and 4 with this option.
#
# Предусматривает установку символьного 4x20 LCD для более детального отображения дополнительной информации.
# Для графических контроллеров 128х64 установка этой опции не обязательна, так как для них информация выводится всегда в четыре строки.
# Пример: CFLAGS += -DFOUR_LINE_LCD
#
# Задает количество символов, выводимых в одну строку для отображения на LCD.
# Следует заметить,что для графических индикаторов 128х64 выводится 16 символов в строку.
# Этот параметр игнорируется для таких индикаторов.
# Пример: CFLAGS += -DLCD_LINE_LENGTH=20
#
#CFLAGS += -DFOUR_LINE_LCD
#CFLAGS += -DLCD_LINE_LENGTH=20

# Some character display types have a different DD_RAM start adress for line 1. 
# Usually the DD_RAM start address for line 1 is 0.
# You can specify a different start address with the option DD_RAM_OFFSET
#DD_RAM_OFFSET=128

# The PAGE_MODE activates a moving line cursor for menu function selection together with FOUR_LINE_LCD
# and WITH_ROTARY_SWITCH.
# Without the PAGE_MODE option, the line cursor is fixed to line 3 and the text moves.
#CFLAGS += -DPAGE_MODE

# The LCD_ST7565 option must be set to support a 128x64 LCD graphics display
# with ST7565 controller. It is controlled with a 1-bit interface (SPI or I2C)
# The normal ST7565 controller will be supported by setting the WITH_LCD_ST7565 to 1 or 7565.
# The special action for a simular SSD1306 controller can be activated by
# setting the WITH_LCD_ST7565 variable to 1306.
#WITH_LCD_ST7565 = 1
#WITH_LCD_ST7565 = 1306

# Normally the ST7565 controller is connected with a SPI 4-wire interface, but
# you can enable a I2C interface with address 0x3c for the SSD1306 controller 
# by setting the LCD_INTERFACE_MODE to 2.
# The SCL signal is available at PD5 (LCD-E, LCD-6), the SDA signal at PD2 (LCD-D6, LCD-13).
# A pull up resistor of about 4.7k is required for both signals to 3.3V.
# Please check, if your display module can also tolerate a 5V signal level.
# For the ST7920 controller you can select the serial interface by setting the LCD_INTERFACE_MODE to 5 . 
# ST7920-RW <--> PD2 , ST7920-E <--> PD5 , ST7920-PSB <--> GND , ST7920-RS <--> VCC , ST7920-RST <--> VCC
# For the PDF8814 controller you can also select a 3 for the 3-line serial interface with RS (D/C) as first bit.
# The RS (data/command) signal at PD1 is used as chip enable SCE.
#CFLAGS += -DLCD_INTERFACE_MODE=2

# With the option LCD_SPI_OPEN_COL the data signals of the SPI interface are not switched to VCC.
# With option LCD_SPI_OPEN_COL the signals are switched to GND only, for high signals the pullup resistors
# of the ATmega are used. For the RESET signal a external pull-up resistor is required, if the
# option PULLUP_DISABLE is set. For the other signals the internal pullup resistors of the ATmega
# are temporary used, even if option PULLUP_DISABLE is set.
#CFLAGS += -DLCD_SPI_OPEN_COL

# The I2C Address can be preset to a address of 0x3d instead of 0x3c by setting the constant LCD_I2C_ADDR.
#CFLAGS += -DLCD_I2C_ADDR=0x3d

# If LCD_ST7565 option is used: Set the resitor ratio for the internal
# voltage regulator. Supported value range: 0..7.
# Good values are e.g. 4 or 7. If unsure just have a try.
LCD_ST7565_RESISTOR_RATIO = 4

# If LCD_ST7565 option is set to 1: Flip the display's horizontal direction.
CFLAGS += -DLCD_ST7565_H_FLIP=1
# With LCD_ST7565_H_OFFSET you can specify a horizontal pixel offset to the display window.
# The controller knows 132 horizontal pixel, the window shows only 128 pixel.
# OFFSET values can vary for the connected display type to 0, 2 or 4.
CFLAGS += -DLCD_ST7565_H_OFFSET=4
# If LCD_ST7565 option is set to 1: Flip the display's vertical direction
CFLAGS += -DLCD_ST7565_V_FLIP=0
# The contrast value can be predefined with the constant VOLUME_VALUE
# for ST7565 controller the value can be between 0 and 63, for the SSD1306 0 to 255 can be selected.
#CFLAGS += -DVOLUME_VALUE=25

# You can specify a Y start line (vertical address) for the display output with the option LCD_ST7565_Y_START.
# If your output start in the middle of the display, you can specify a Y_START of 32
#CFLAGS += -DLCD_ST7565_Y_START=32

# If option WITH_LCD_ST7565 is present one of the following fonts should be
# choosen. With a font width below 8 more than 16 characters can be shown in one display line.
#CFLAGS += -DFONT_5X8
#CFLAGS += -DFONT_6X8
#CFLAGS += -DFONT_8X8
CFLAGS += -DFONT_7X12
#CFLAGS += -DFONT_8X12thin
#CFLAGS += -DFONT_8X14
#CFLAGS += -DFONT_8x15
#CFLAGS += -DFONT_8X16
#CFLAGS += -DFONT_8X16thin

# There are also different 24x32 pixel icons for presentation of the transistor symbols available.
# you can select a special type with setting the ICON_TYPE.
# Currently you can select 1 or 3 for one of two thin layouts for the icons.
# You can also select two thick layouts for the icons by setting the ICON_TYPE to 2 or 0 (0=old style).
CFLAGS += -DICON_TYPE=3

# option BIG_TP makes the 123 for the test pins (beside the icon) bigger
CFLAGS += -DBIG_TP
# option INVERSE_TP inverse the 123 for the test pins (black on white)
# the option INVERSE_TP disable the option BIG_TP because a frame is required
#CFLAGS += -DINVERSE_TP

# Option STRIP_GRID_BOARD selects different board-layout, do not set for standard board!
# The connection of LCD is totally different for both versions.
#
# Эта опция позволяет изменить назначения выводов порта D для подключения дисплея.
# Более подробное описание Вы можете найти в описании аппаратных средств главы 2.1 на странице 9.
# Вы также можете выбрать альтернативное подключение выводов ATmega к графическому индикатору.
# Для китайского клона «T5» Вы должны установить значение STRIP_GRID_BOARD=5.
# При альтернативном назначении контактов для графического дисплея подключение кнопки остается неизменным.
#CFLAGS += -DSTRIP_GRID_BOARD

# The WITH_SELFTEST option enables selftest function (only for mega168 or mega328) including the calibration.
# Normally the mega168 uses selftest without T1 to T7 to enable both hFE measurements.
#
# Если Вы выбираете эту опцию, программное обеспечение будет включать функцию самодиагностики.
# Самодиагностика будет начата,если Вы соедините все 3 испытательных порта вместе «перемычкой» и нажмете кнопку TEST.
# Если функция выбрана, запускается только калибровка. 
# Самодиагностика T1 - T7 возможна только при выборе функции из дополнительного меню.
CFLAGS += -DWITH_SELFTEST

# You can enable the extended tests T1 to T7 for the atmega168 by selecting the  NO_COMMON_COLLECTOR_HFE  option.
# The T1 to T7 tests are usefull to find problems with your tester.
# You can also disable the extended tests T1 to T7 with the option NO_TEST_T1_T7 to accelerate the calibration
# for the atmega328 and atmega168.
#
# Эта опция отключает выполнение функций самодиагностики Т1 - Т7.
# Эти тесты самодиагностики полезны для обнаружения ошибок в аппаратных средствах, например,неправильного измерения сопротивлений или проблемы с изоляцией.
# Если Вы уверены,что оборудование исправно, то для ускорения калибровки Вы можете пропустить самодиагностику Т1 - Т7, установив эту опцию.
# При включенной опции тесты Т1- Т7 самодиагностики запускаются только из дополнительного меню «Selftest».
# Если с микроконтроллером ATmega168 используются оба метода измерения hFE,то функции самодиагностики T1 - T7 пропускается автоматически.
#CFLAGS += -DNO_TEST_T1_T7

# FREQUENCY_50HZ enables a 50 Hz frequency generator for up to one minute at the end of selftests.
#
# Сигнал 50 Гц будет генерироваться на выводах испытательных пор-тов 2 и 3 в течении одной минуты в конце самодиагностики.
# Эта опция должна быть установлена только для особых случаев - проверки функции задержки.
#CFLAGS += -DFREQUENCY_50HZ

# Эта опция отключает метод измерения hFE транзисторов по схеме с общим коллектором.
# По умолчанию включены оба метода для измерения hFE, но в памяти программ микроконтроллера ATmega168 не хватает места для функций самодиагностики.
# С помощью этой опции Вы можете освободить память микроконтроллера ATmega168 для функций самодиагностики T1-T7.
#CFLAGS += -DNO_COMMON_COLLECTOR_HFE
#
# Эта опция отключает метод измерения hFE транзисторов по схеме с общим эмиттером.
# По умолчанию включены оба метода для измерения hFE, но в памяти программ микроконтроллера ATmega168 не хватает места для функций самодиагностики.
# С помощью этой опции Вы можете освободить память микроконтроллера ATmega168 для функций самопроверки T1-T7.
#CFLAGS += -DNO_COMMON_EMITTER_HFE

# AUTO_CAL will enable the autocalibration of zero offset of capacity measurement and
# also the port output resistance values will be find out in SELFTEST section.
# With a external capacitor a additionally correction of reference voltage is figured out for 
# low capacity measurement and also for the AUTOSCALE_ADC measurement.
# The AUTO_CAL option is only selectable for mega168 and mega328.
#
# В процедуре самодиагностики будет дополнительно измерено смещение нуля при измерении ёмкости.
# Дополнительно будут измерены смещение аналогового компаратора (REF_C_KORR) и (REF_R_ KORR) напряжение смещения внутреннего опорного напряжения,
# если Вы подключите качественный конденсатор с величиной ёмкости от 100нФ до 20мкФ 𝜈к выводам испытательных портов 1 и 3 после измерения смещения нуля при измерении ёмкости.
# Все найденные величины будут записаны в EEprom и будут использоваться для дальнейших измерений автоматически.
# Значения выходного сопротивления порта будут определяться в начале каждого измерения.
CFLAGS += -DAUTO_CAL

# The tester reports the uncalibrated state with a message after testing a part.
# Normally a long text is shown, which explains the steps of calibration.
# You can prevent the long explanation by setting the SHORT_UNCAL_MSG option.
# With this option set, only a hint of one line is shown.
#CFLAGS += -DSHORT_UNCAL_MSG

# You can extend the measurement feature by use of a sampling mode for the ADC converter
# to extend the resolution of capacity measurement to about 0.01pF.
# Setting the WITH_SamplinADC to 1 enables this feature for capacity values below 100pF.
WITH_SamplingADC = 1

# Option WITH_XTAL enables additional Xtal / Ceramic resonator tests.
# Option can be set only together with SamplingADC=1 and OP_MHZ=16
#CFLAGS += -DWITH_XTAL 
# Option WITH_UJT enables additional tests for UJT (UniJunction Transistor)
CFLAGS += -DWITH_UJT
# Option WITH_PUT enables additional tests for PUT (Programmable Unijunction Transistor)
CFLAGS += -DWITH_PUT
# Option FET_Idss will measure the Idss parameter for FETs, if not estimated > 40mA.
CFLAGS += -DFET_Idss

# The WITH_AUTO_REF option enables reading of internal REF-voltage to get factors for the Capacity measuring.
CFLAGS += -DWITH_AUTO_REF
# REF_C_KORR corrects the reference Voltage for capacity measurement (<40uF) and has mV units.
# Greater values gives lower capacity results.
CFLAGS += -DREF_C_KORR=12
# REF_L_KORR corrects the reference Voltage for inductance measurement and has mV units.
CFLAGS += -DREF_L_KORR=40
# C_H_KORR defines a correction of 0.1% units for big capacitor measurement.
# Positive values will reduce measurement results.
CFLAGS += -DC_H_KORR=0

# The WITH_UART option enables the software UART  (TTL level output at Pin PC3, 26).
# You can set WITH_UART to 2 to enable a special mode of serial output with line number in column 1.
# If the option is deselected, PC3 can be used as external voltage input with a
# 10:1 resistor divider.
#CFLAGS += -DWITH_UART

# With option TQFP_ADC6 or/and TQFP_ADC7 you can use the additional pins of the TQFP or
# the QFN package for external analog input. You should install a 10:1 voltage dividers
# on the selected pin(s).
# If both pins are defined, both voltages are measured with the voltage measure function.
# But for zener diode measurement the ADC6 pin is used, if both pins are defined.
#CFLAGS += -DTQFP_ADC6

# For ATmega8/168/328 processor the option WITH_VEXT can only be set, if the PC3 pin
# is not used for serial output (WITH_UART option).
# For ATmega644/1284 processor the UART has a separate pin.  Therefore the external input
# at pin ADC3 can be enabled separate by setting the WITH_UART option.
CFLAGS += -DWITH_VEXT

#
# If you want to measure Inductors with the resistance meter, you must specify
# the RMETER_WITH_L  option. The measurement cycle time slow down with this option
# for resistors below 2.1kOhm. Resistors below 10 Ohm are measured additionally
# with the ESR measurement methode, which takes also a longer time.
CFLAGS += -DRMETER_WITH_L

# The CAP_EMPTY_LEVEL  defines the empty voltage level for capacitors in mV.
# Choose a higher value, if your Tester reports "Cell!" by unloading capacitors.
CFLAGS += -DCAP_EMPTY_LEVEL=4

# The AUTOSCALE_ADC option enables the autoscale ADC (ADC use VCC and Bandgap Ref).
CFLAGS += -DAUTOSCALE_ADC
CFLAGS += -DREF_R_KORR=3

# The ESR_ZERO value define the zero value of ESR measurement (units = 0.01 Ohm).
#CFLAGS += -DESR_ZERO=29
CFLAGS += -DESR_ZERO=20

# NO_AREF_CAP tells your Software, that you have no Capacitor installed at pin AREF (21).
# This enables a shorter wait-time for AUTOSCALE_ADC function.
# A capacitor with 1nF can be used with the option NO_AREF_CAP set.
CFLAGS += -DNO_AREF_CAP

# The OP_MHZ option tells the software the Operating Frequency of your ATmega.
#!!
#OP_MHZ = 8
OP_MHZ = 20

# Restart from sleep mode will be delayed for 16384 clock tics with crystal mode.
# Operation with the internal RC-Generator or external clock will delay the restart by only 6 clock tics.
# You must specify this with "CFLAGS += -DRESTART_DELAY_TICS=6", if you don't use the crystal mode.
#CFLAGS += -DRESTART_DELAY_TICS=6

# The USE_EEPROM option specify where you wish to locate fix text and tables.
# If USE_EEPROM is unset, program memory (flash) is taken for fix text and tables.
CFLAGS += -DUSE_EEPROM

# Setting EBC_STYPE will select the old style to present the order of Transistor connection (EBC=...).
# Omitting the option will select the 123=... style.  Every point is replaced by a character identifying 
# type of connected transistor pin (B=Base, E=Emitter, C=Collector, G=Gate, S=Source, D=Drain).
# If you select EBC_STYLE=321 , the style will be 321=... , the inverted order to the 123=... style.
#CFLAGS += -DEBC_STYLE
#CFLAGS += -DEBC_STYLE=321

# Setting of NO_NANO avoids the use of n as prefix for Farad (nF), the mikro prefix is used instead (uF).
# CFLAGS += -DNO_NANO

# With graphical displays the layout of pins is usually shown in long style " Pin  1=E 2=B 3=C"
# With the NO_LONG_PINLAYOUT option the short style "Pin 123=EBC" is used
#CFLAGS += -DNO_LONG_PINLAYOUT

# The PULLUP_DISABLE option disable the pull-up Resistors of IO-Ports.
# To use this option a external pull-up Resistor (10k to 30k)
# from Pin 13 to VCC must be installed!
CFLAGS += -DPULLUP_DISABLE

# The ANZ_MESS option specifies, how often an ADC value is read and accumulated.
# Possible values of ANZ_MESS are 5 to 200 .
CFLAGS += -DANZ_MESS=25


# The POWER_OFF option enables the power off function, otherwise loop measurements infinitely
# until power is disconnected with a ON/OFF switch (CFLAGS += -DPOWER_OFF).
# If you have the tester without the power off transistors, you can deselect POWER_OFF .
# If you have NOT selected the POWER_OFF option with the transistors installed,
# you can stop measuring by holding the key several seconds after a result is
# displayed. After releasing the key, the tester will be shut off by timeout.
# Otherwise you can also specify, after how many measurements without found part
# the tester will shut down (CFLAGS += -DPOWER_OFF=5).
# The tester will also shut down with found part,
# but successfull measurements are allowed double of the specified number.
#  You can specify up to 255 empty measurements (CFLAGS += -DPOWER_OFF=255).
#
# Эта опция включает функцию автоматического выключения питания.
# Если Вы не установите эту опцию, измерения будут идти бесконечно, пока не будет отключено питание прибора.
# Если у Вас тестер без схемы отключения питания, то Вы можете не выбирать POWER_OFF.
# Если Вы не установили опцию POWER_OFF для прибора с авто отключением, то тестер можно выключить из меню выбора функций при активизированной опции WITH_MENU.
# Вы можете также определить,после скольких измерений без определения элемента тестер выключится.
# Тестер также отключит питание после вдвое большего числа измерений, сделанных последовательно без неудавшегося поиска элемента.
# Это позволяет избежать полного разряда батареи, если Вы забыли отсоединять тестируемый элемент.
# Выбор определяется как CFLAGS += -DPOWER_OFF=5 для 5 последовательных измерений без определения элемента.
# Тестер также выключится после 10 измерений с определением элемента.
# Если любая последовательность измерений будет прервана другим типом, то измерения продолжатся.
# Результат измерения отображается на дисплее в течение 28 секунд для однократного измерения, 
# для многократного измерения время отображения уменьшено до 5 секунд (выбор в config.h).
# Если кнопка TEST нажата более длительное время, то время отображения для многократного измерения также 28 секунд. # Максимальное значение 255 (CFLAGS +=-DPOWER_OFF=255).
#CFLAGS += -DPOWER_OFF=5
CFLAGS += -DPOWER_OFF

# Option BAT_CHECK enables the Battery Voltage Check, otherwise the SW Version is displayed instead of Bat.
# BAT_CHECK should be set for battery powered tester version.
#
# Позволяет проверять напряжение батареи питания. Если Вы НЕ выбираете эту опцию,
# то на LCD дисплее вместо напряжения будет отображаться номер версии программного обеспечения. 
# Эта опция полезна для версии тестера,работающей от автономного источника питания,
# чтобы напомнить о разряде источника питания.
#!!
#CFLAGS += -DBAT_CHECK

# The BAT_OUT option enables Battery Voltage Output on LCD (if BAT_CHECK is selected).
# If your 9V supply has a diode installed, use the BAT_OUT=600 form to specify the
# threshold voltage of your diode to adjust the output value.
# This threshold level is added to LCD-output and does not affect the voltage checking levels.
#
# Позволяет отображать напряжение батареи на LCD дисплее (если выбрана опция BAT_CHECK).
# Если в цепи питания 9В установлен диод, то для правильного измерения выходного значения
# необходимо учесть напряжение падения на нем (в мВ), для этого используйте BAT_OUT=600.
# Также этой опцией можно учитывать падение напряжения на транзисторе  T3.
# Пороговый уровень не влияет на уровни проверки напряжения (BAT_POOR).
# Пример 1: CFLAGS += -DBAT_OUT=300 # Пример 2: CFLAGS += -DBAT_OUT
CFLAGS += -DBAT_OUT=150

# To adjust the warning-level and poor-level of battery check to the capability of a
# low drop voltage regulator, you can specify the Option BAT_POOR=5400 .
# The unit for this option value is 1mV , 5400 means a poor level of 5.4V.
# The warning level is 0.8V higher than the specified poor level (>5.3V).
# The warning level is 0.4V higher than the specified poor level (>2.9V, <=5.3V).
# The warning level is 0.2V higher than the specified poor level (>1.3V, <=2.9V).
# The warning level is 0.1V higher than the specified poor level (<=1.3V).
# Setting the poor level to low values is not recommended for rechargeable Batteries,
# because this increase the danger for deep discharge!!
#
# Установка нижнего уровня напряжения батареи, задаваемого в мВ.
# Если нижний уровень составляет больше чем 5,3В, то уровень предупреждения о разряде батареи на 0,8В выше, чем указанный нижний уровень.
# Если нижний уровень составляет 5,3В𝑊или менее, то уровень предупреждения о разряде батареи на 0,4В𝑊выше, чем указанный нижний уровень.
# Если нижний уровень ниже 3,25В, то уровень предупреждения о разряде батареи на 0,2В выше,чем указанный нижний уровень.
# Если нижний уровень ниже 1,3В, то уровень предупреждения о разряде батареи на 0,1В выше, чем указанный нижний уровень.
# Установка нижнего уровня 5,4В не рекомендуется для перезаряжаемых 9В аккумуляторов, потому что это увеличивает риск повреждения аккумулятора из-за глубокого разряда !
# Если Вы хотите использовать 9В аккумулятор, то рекомендуется использовать Ready To Use тип аккумулятора из-за более низкого саморазряда.
# Пример для low drop regulator (5, 4 𝑊 ): CFLAGS += -DBAT_POOR=5400
# Пример для 7805 type regulator (6, 4 𝑊 ): CFLAGS += -DBAT_POOR=6400
#!!
CFLAGS += -DBAT_POOR=5400

# You can set a upper battery voltage limit in mV units for battery operation mode.
# The operation time of additional functions is limited with the battery operation mode. 
# Above the voltage limit "DC_PWR" the tester changes the operation mode to the
# "DC_Pwr_Mode", where time limits of the additional functions are switched off.
# The "DC_Pwr_Mode" is also started, if the battery voltage is detected below 0.9V
# regardless to the state of the DC_PWR option.
#
# Уровень напряжения в мВ измеренного при тесте напряжения питания тестера, выше которого устанавливается режим «DC_Pwr_Mode».
# Обычно тестер работает от батареи и при этом все дополнительные функции ограничены во времени.
# В режиме «DC_Pwr_Mode»,предполагается,что тестер работает от внешнего блока питания, поэтому дополнительные функции работают без ограничения по времени.
# Потому что DC-DC преобразователь не работает при входном напряжении меньше 0.9В,
# режим «DC_Pwr_Mode» также устанавливается, если обнаружено напряжение питания бата-реи ниже 0.9В.
# Пример: CFLAGS += -DDC_PWR=9500
# CFLAGS += -DDC_PWR=9500

# Voltage divider for battery voltage measurement  10k / 3.3k = 133/33
#
# Делитель напряжения для измерения напряжения батареи 10k/3.3k = 133/33
#CFLAGS += -DBAT_NUMERATOR=133
#CFLAGS += -DBAT_DENOMINATOR=33

# Voltage divider for the external zener voltage measurement 180k / 20k = 10/1
#
# Делитель напряжения для внешнего измерения стабилитрон напряжение 180K / 20k = 10/1
#CFLAGS += -DEXT_NUMERATOR=10
#CFLAGS += -DEXT_DENOMINATOR=1

# The sleep mode of the ATmega168 or ATmega328 is normally used by the software to save current.
# You can inhibit this with the option INHIBIT_SLEEP_MODE .
#
# Запрещает использование SLEEP_MODE. 
# Обычно программное обеспечение использует SLEEP_MODE для более длительной работы.
# Использование этого способа действительно экономит заряд батареи, но создает дополнительную нагрузку для стабилизатора напряжения.
# Пример: INHIBIT_SLEEP_MODE = 1 (для версий до 290)
# Пример: INHIBIT_SLEEP_MODE = 0 (для версии 291 и выше)
INHIBIT_SLEEP_MODE = 0


# Select your programmer type, speed and port, if you wish to use avrdude.
# setting for DIAMEX ALL_AVR, Atmel AVRISP-mkII
#PROGRAMMER=avrisp2
#BitClock=5.0
#PORT=usb
# setting for USBasp
#PROGRAMMER=usbasp
#BitClock=20
#PORT=usb
# setting for ARDUINO MEGA, requires bootloader
#PROGRAMMER=wiring
#PORT = /dev/ttyACM0
#BitClock=5.0
#AVRDUDE_BAUD = -b 115200 -D
# For STK500 HWProgUSB https://github.com/74ls00/HVProgUSB
PROGRAMMER=stk500v2
PORT=com7
BitClock=1




# ********************** end of selectable options

include ../setup.mk

########### Compile only Assembler source available 
lcd_hw_4_bit.o: ../lcd_hw_4_bit.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

wait1000ms.o: ../wait1000ms.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

swuart.o: ../swuart.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

########### Compile  Assembler source only, is time critical 
GetESR.o: ../GetESR.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

########### Compile C or Assembler , Assembler saves more than 400 bytes flash
GetRLmultip.o: ../GetRLmultip.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

UfAusgabe.o: ../UfAusgabe.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

RvalOut.o: ../RvalOut.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

PinLayout.o: ../PinLayout.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

RefVoltage.o: ../RefVoltage.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

i2lcd.o: ../i2lcd.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

ReadADC.o: ../ReadADC.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

sleep_5ms.o: ../sleep_5ms.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

wait_for_key_ms.o: ../wait_for_key_ms.c $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

get_log.o: ../get_log.S $(MKFILES)
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

include ../finish.mk
