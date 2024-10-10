# Структура каталогов

## Корневой каталог проекта

`/project-name/`

## Каталоги проекта

`/project-name/compiler-name` - содержит файл workspace и прочие, необходимые и генерируемые IDE при создании проекта

`/project-name/compiler-name/app` - файлы `main` и `version_file.h`

`/project-name/lib` - сторонние библиотеки (желательно подключённые как `submodules`)

`/project-name/inc` - заголовочные файлы

`/project-name/src` - source файлы (`*.c` и `*.cpp`)

`/project-name/tests` - файлы для тестирования

---------------------------------------------------------

# Version File

Заголовочный файл, содержащий версию прошивки.

Пример определения файла

```c
#undef VERSION
#define VERSION "Version 1.30"
```

Пример содержания:

```c
/***
Version Module-Project SAMPLE

Copyright 2007 Company
All Rights Reserved

The information contained herein is confidential
property of Company. The use, copying, transfer or
disclosure of such information is prohibited except
by express written agreement with Company.

12/18/07-Version 1.3-ROM ID 78-130
    Modified module AD_TO_D to fix scaling
    algorithm; instead of y = mx, it now
    computes y =mx+ b.
10/29/07-Version 1.2-ROM ID 78-120
    Changed modules DISPLAY_LED and READ_DIP
    to incorporate marketing ’s request for a
    diagnostics mode.
09/03/07-Version 1.1-ROM ID 78-110
    Changed module ISR to properly handle
    non-reentrant math problem.
07/12/07-Version 1.0-ROM ID 78-100
    Initial release
***/
#undef VERSION
#define VERSION "Version 1.30"
```

**Примечание** - в IAR попробовал просто define, но не получилось прочитать такую строку через J-Flasher. Удачная попытка была только при объявлении **локальной** переменной в `main()`.

# Структура отдельных файлов

## Source Files

### Структура файла

1) Блок комментариев
3) Includes
4) Defines
5) Enums
6) Structs
7) Unions
8) Typedefs
5) константы
6) объявление static переменных
7) прототипы private функций
8) определения public функций, объявленных в заголовочном файле
9)  определения private функций


### Шаблон

```c
 /**
 * @file header.c
 * @author Chel Mik (chel_m@mail.ru)
 * @brief 
 * @version 0.1
 * @date 2000-00-00
 * 
 * @copyright Copyright (c) 2000
 * 
 */


/** @defgroup Includes */
/** @{ */

#include "header.h"

/** @} */


/** @defgroup Defines */
/** @{ */

#define VOLGA 0

#define ABS(X) ((X) > 0 ? (X) : (-(X)))

/** @} */

/** @defgroup Enums */
/** @{ */

/** @} */


/** @defgroup Structs */
/** @{ */

/** @} */


/** @defgroup Unions */
/** @{ */

/** @} */


/** @defgroup Typedefs */
/** @{ */

/**
  * @brief  Числа
  */
typedef enum {
    one,    /*!< Один */
    two,    /*!< Два */
} NUMS;

/** @} */

/** @defgroup Constants */
/** @{ */

const char *s = "Const";

/** @} */


/** @defgroup Variables */
/** @{ */

int big = 1000;

static small = 10;

/** @} */


/** @defgroup Prototypes of Private Functions */
/** @{ */

void func_priv(int num1, int num2);

/** @} */


/** @defgroup Public Functions */
/** @{ */

/**
  * @brief   Настройка частоты SCL врежиме FS
  * @param   num1  Первый параметр
  * @param   num2  Второй параметр
  * @retval  void
  */
void func(int num1, int num2)
{

}

/** @} */


/** @defgroup Private Functions */
/** @{ */

/**
  * @brief   Настройка частоты SCL врежиме FS
  * @param   num1  Первый параметр
  * @param   num2  Второй параметр
  * @retval  void
  */
void func_priv(int num1, int num2)
{

}

/** @} */

```

## Заголовочные файлы

### Структура файла

1) Блок комментариев
2) Защита от множественного включения файла
3) Обёртка при использовании C++
4) Includes
5) Defines
6) Enums
7) Structs
8) Unions
9) Typedefs
10) определения public функций
11) Extern константы 
12) Extern переменные

### Шаблон

```c
 /**
 * @file header.h
 * @author Chel Mik (chel_m@mail.ru)
 * @brief 
 * @version 0.1
 * @date 2000-00-00
 * 
 * @copyright Copyright (c) 2000
 * 
 */

#ifndef HEADER_H
#define HEADER_H

#ifdef __cplusplus
extern "C" {
#endif


/** @defgroup Includes */
/** @{ */

#include <stdint.h>

/** @} */


/** @defgroup Defines */
/** @{ */

#define BIBA 0X01

/** @} */


/** @defgroup Enums */
/** @{ */

/** @} */


/** @defgroup Structs */
/** @{ */

/** @} */


/** @defgroup Unions */
/** @{ */

/** @} */


/** @defgroup Typedefs */
/** @{ */

/**
  * @brief  Числа
  */
typedef enum {
    one,    /*!< Один */
    two,    /*!< Два */
} NUMS;

/** @} */


/** @defgroup Prototypes of Public Functions */
/** @{ */

/**
  * @brief   Настройка частоты SCL врежиме FS
  * @param   num1  Первый параметр
  * @param   num2  Второй параметр
  * @retval  void
  */
void func(int num1, int num2);

/** @} */


/** @defgroup Extern Constants */
/** @{ */

/** @} */


/** @defgroup Extern Variables */
/** @{ */

extern int Var;

/** @} */


#ifdef __cplusplus
}
#endif

#endif // HEADER_H
```