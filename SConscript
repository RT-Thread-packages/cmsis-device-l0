from building import *
import os

# Import environment variables
Import('env')

# Get the current working directory
cwd = GetCurrentDir()

# Initialize include paths and source files list
path = [os.path.join(cwd, 'Include')]
src = [os.path.join(cwd, 'Source', 'Templates', 'system_stm32l0xx.c')]

# Map microcontroller units (MCUs) to their corresponding startup files
mcu_startup_files = {
    'STM32L010x4': 'startup_stm32l010x4.s',
    'STM32L010x6': 'startup_stm32l010x6.s',
    'STM32L010x8': 'startup_stm32l010x8.s',
    'STM32L010xB': 'startup_stm32l010xb.s',
    'STM32L011xx': 'startup_stm32l011xx.s',
    'STM32L021xx': 'startup_stm32l021xx.s',
    'STM32L031xx': 'startup_stm32l031xx.s',
    'STM32L041xx': 'startup_stm32l041xx.s',
    'STM32L051xx': 'startup_stm32l051xx.s',
    'STM32L052xx': 'startup_stm32l052xx.s',
    'STM32L053xx': 'startup_stm32l053xx.s',
    'STM32L062xx': 'startup_stm32l062xx.s',
    'STM32L063xx': 'startup_stm32l063xx.s',
    'STM32L071xx': 'startup_stm32l071xx.s',
    'STM32L072xx': 'startup_stm32l072xx.s',
    'STM32L073xx': 'startup_stm32l073xx.s',
    'STM32L081xx': 'startup_stm32l081xx.s',
    'STM32L082xx': 'startup_stm32l082xx.s',
    'STM32L083xx': 'startup_stm32l083xx.s',
}

# Check each defined MCU, match the platform and append the appropriate startup file
cpp_defines_tuple = env.get('CPPDEFINES', [])
cpp_defines_list = [item[0] if isinstance(item, tuple) else item for item in cpp_defines_tuple]
for mcu, startup_file in mcu_startup_files.items():
    if mcu in cpp_defines_list:
        if rtconfig.PLATFORM in ['gcc', 'llvm-arm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'gcc', startup_file)]
        elif rtconfig.PLATFORM in ['armcc', 'armclang']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'arm', startup_file)]
        elif rtconfig.PLATFORM in ['iccarm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'iar', startup_file)]
        break

# Define the build group
group = DefineGroup('STM32L0-CMSIS', src, depend=['PKG_USING_STM32L0_CMSIS_DRIVER'], CPPPATH=path)

# Return the build group
Return('group')
