# Инструкция по установке Microsoft Office с выборочными компонентами

Полное руководство по скачиванию, установке и активации Microsoft Office с минимальным набором приложений.

> **Примечание:**  
> Если вам нужны только Word, Excel и PowerPoint, переходите сразу [к шагу 3](#-шаг-3-подготовка-к-установке).

## 📋 Требования

* Права администратора на устройстве
* Windows 10/11 (64-bit)
* Стабильное интернет-соединение
* 4 ГБ свободного места на диске

## 🛠️ Шаг 1: Подготовка инструментов

Скачайте распаковщик [Office Deployment Tool (ODT)](https://www.microsoft.com/en-us/download/details.aspx?id=49117) с официального сайта.

Запустите распаковщик и укажите папку для распаковки ODT.

> После распаковки в папке должен быть установщик `setup.exe` и файл конфигурации с расширением `.xml`

## ⚙️ Шаг 2: Настройка конфигурации

Создайте `configuration.xml` рядом с `setup.exe` со следующим содержимым:

```xml
<Configuration>
  <Add OfficeClientEdition="64" Channel="Broad">
    <Product ID="O365ProPlusRetail">
      <Language ID="MatchOS" />
      <ExcludeApp ID="Access" />
      <ExcludeApp ID="Groove" />
      <ExcludeApp ID="Lync" />
      <ExcludeApp ID="OneDrive" />
      <ExcludeApp ID="OneNote" />
      <ExcludeApp ID="Outlook" />
      <ExcludeApp ID="Publisher" />
      <ExcludeApp ID="Teams" />
    </Product>
  </Add>
  <RemoveMSI />
</Configuration>
```

> **Альтернативный метод:**
> Использовать [онлайн-конфигуратор от Microsoft](https://config.office.com/deploymentsettings)

## 📥 Шаг 3: Подготовка к установке

> **Примечание:**
> При скачивании с российских IP возникает ошибка `Command Not Supported`. Для её решения в `PowerShell` необходимо ввести команду:

```PowerShell
reg add "HKCU\Software\Microsoft\Office\16.0\Common\ExperimentConfigs\Ecs" /v "CountryCode" /t REG_SZ /d "std::wstring|US" /f
```

Запустите `PowerShell` от имени администратора в папке с файлами и выполните:

```PowerShell
./setup /download configuration.xml
```

Дождитесь завершения (размер папки `Office` ~3.13 ГБ)


## 💻 Шаг 4: Установка

В том же окне выполните:

```PowerShell
./setup /configure configuration.xml
```

## 🔑 Шаг 5: Активация

В том же окне выполните:

```PowerShell
irm https://get.activated.win | iex
```

В меню скрипта:
1. Выберете `2` [Ohook]
2. Затем `1` [Install Ohook Office Activation]

Дождитесь выполнения активации.
