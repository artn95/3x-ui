# 3X-UI



<p align="center"><a href="#"><img src="./media/3X-UI.png" alt="Image"></a></p>

**Расширенная веб-панель • Построена на Xray Core**

[![](https://img.shields.io/github/v/release/artn95/3x-ui.svg)](https://github.com/artn95/3x-ui/releases)
[![](https://img.shields.io/github/actions/workflow/status/artn95/3x-ui/release.yml.svg)](#)
[![GO Version](https://img.shields.io/github/go-mod/go-version/artn95/3x-ui.svg)](#)
[![Downloads](https://img.shields.io/github/downloads/artn95/3x-ui/total.svg)](#)
[![License](https://img.shields.io/badge/license-GPL%20V3-blue.svg?longCache=true)](https://www.gnu.org/licenses/gpl-3.0.en.html)


## Установить и обновить

```
bash <(curl -Ls https://raw.githubusercontent.com/artn95/3x-ui/master/install.sh) 
```

## Установить Пользовательскую Версию

Чтобы установить нужную версию, добавьте версию в конец команды установки. например, версия `v2.2.6`:

```
bash <(curl -Ls https://raw.githubusercontent.com/artn95/3x-ui/master/install.sh) v2.2.6
```

## SSL сертификат

<details>
  <summary>Нажмите для получения SSL-сертификата</summary>

### Облачная вспышка

Скрипт управления имеет встроенное приложение SSL-сертификата для Cloudflare. Чтобы использовать этот скрипт для подачи заявки на сертификат, вам нужно следующее:

- Электронная почта, зарегистрированная Cloudflare
- Глобальный ключ API Cloudflare
- Доменное имя было разрешено текущему серверу через cloudflare

**1:** Запустите `x-ui`на терминале, затем выберите `Cloudflare SSL Certificate`.


### Certbot
```
apt-get install certbot -y
certbot certonly --standalone --agree-tos --register-unsafely-without-email -d (добовляем свой домен)
certbot renew --dry-run
```

***Tip:*** *Certbot также встроен в скрипт управления. Вы можете запустить команду `x-ui` а затем выбрать `SSL Certificate Management`.*

</details>

## Ручная установка и обновление

<details>
  <summary>Нажмите для получения подробной информации об установке вручную</summary>

#### Использование

1. Чтобы загрузить последнюю версию сжатого пакета непосредственно на ваш сервер, выполните следующую команду:

```sh
ARCH=$(uname -m)
case "${ARCH}" in
  x86_64 | x64 | amd64) XUI_ARCH="amd64" ;;
  i*86 | x86) XUI_ARCH="386" ;;
  armv8* | armv8 | arm64 | aarch64) XUI_ARCH="arm64" ;;
  armv7* | armv7) XUI_ARCH="armv7" ;;
  armv6* | armv6) XUI_ARCH="armv6" ;;
  armv5* | armv5) XUI_ARCH="armv5" ;;
  *) XUI_ARCH="amd64" ;;
esac


wget https://github.com/artn95/3x-ui/releases/latest/download/x-ui-linux-${XUI_ARCH}.tar.gz
```

2. После загрузки сжатого пакета выполните следующие команды для установки или обновления x-ui:

```sh
ARCH=$(uname -m)
case "${ARCH}" in
  x86_64 | x64 | amd64) XUI_ARCH="amd64" ;;
  i*86 | x86) XUI_ARCH="386" ;;
  armv8* | armv8 | arm64 | aarch64) XUI_ARCH="arm64" ;;
  armv7* | armv7) XUI_ARCH="armv7" ;;
  armv6* | armv6) XUI_ARCH="armv6" ;;
  armv5* | armv5) XUI_ARCH="armv5" ;;
  *) XUI_ARCH="amd64" ;;
esac

cd /root/
rm -rf x-ui/ /usr/local/x-ui/ /usr/bin/x-ui
tar zxvf x-ui-linux-${XUI_ARCH}.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

</details>

## Установить с помощью Docker

<details>
  <summary>Нажмите для получения подробной информации о Docker</summary>

#### Использование

1. Установить Docker:

   ```sh
   bash <(curl -sSL https://get.docker.com)
   ```

2. Клонировать репозиторий проекта:

   ```sh
   git clone https://github.com/artn95/3x-ui.git
   cd 3x-ui
   ```

3. Запустить сервис

   ```sh
   docker compose up -d
   ```

   ИЛИ

   ```sh
   docker run -itd \
      -e XRAY_VMESS_AEAD_FORCED=false \
      -v $PWD/db/:/etc/x-ui/ \
      -v $PWD/cert/:/root/cert/ \
      --network=host \
      --restart=unless-stopped \
      --name 3x-ui \
      ghcr.io/artn95/3x-ui:latest
   ```

обновить до последней версии

   ```sh
    cd 3x-ui
    docker compose down
    docker compose pull 3x-ui
    docker compose up -d
   ```

удалить 3x-ui из докера 

   ```sh
    docker stop 3x-ui
    docker rm 3x-ui
    cd --
    rm -r 3x-ui
   ```

</details>


## Рекомендуемая ОС

- Ubuntu 20.04+
- Debian 11+
- CentOS 8+
- Fedora 36+
- Arch Linux
- Manjaro
- Armbian
- AlmaLinux 9+
- Rockylinux 9+

## Поддерживаемые архитектуры и устройства

<details>
  <summary>Нажмите для получения подробной информации о поддерживаемых архитектурах и устройствах</summary>

Наша платформа обеспечивает совместимость с различными архитектурами и устройствами, обеспечивая гибкость в различных вычислительных средах. Ниже приведены ключевые архитектуры, которые мы поддерживаем:

- **amd64**: Эта распространенная архитектура является стандартом для персональных компьютеров и серверов, беспрепятственно вмещая большинство современных операционных систем.

- **x86 / i386**: Широко распространенная в настольных и портативных компьютерах, эта архитектура пользуется широкой поддержкой многочисленных операционных систем и приложений, включая, помимо прочего, системы Windows, macOS и Linux.

- **armv8 / arm64 / aarch64**: Эта архитектура, адаптированная для современных мобильных и встроенных устройств, таких как смартфоны и планшеты, является примером таких устройств, как Raspberry Pi 4, Raspberry Pi 3, Raspberry Pi Zero 2/Zero 2 W, Orange Pi 3 LTS и многое другое.

- **armv7 / arm / arm32**: Выступая в качестве архитектуры для старых мобильных и встроенных устройств, он по-прежнему широко используется в таких устройствах, как Orange Pi Zero LTS, Orange Pi PC Plus, Raspberry Pi 2 и других.

- **armv6 / arm / arm32**: Эта архитектура, ориентированная на очень старые встроенные устройства, хотя и менее распространена, все еще используется. Такие устройства, как Raspberry Pi 1, Raspberry Pi Zero/Zero W, полагаются на эту архитектуру.

- **armv5 / arm / arm32**: Старая архитектура, в основном связанная с ранними встроенными системами, сегодня она менее распространена, но все еще может быть найдена в устаревших устройствах, таких как ранние версии Raspberry Pi и некоторые старые смартфоны.
</details>

## Языки

- английский
- Французкий
- Китайский
- Русский
- Вьетнамский
- Испанский
- Индонезийский 
- Украинский


## ХАРАКТЕРИСТИКИ

- Мониторинг Состояния Системы
- Поиск по всем входящим и клиентам
- Темная/светлая тема
- Поддерживает многопользовательский и многопротокольный
- Поддерживает протоколы, включая VMess, VLESS, Trojan, Shadowsocks, Dokodemo-door, Socks, HTTP, wireguard
- Поддерживает собственные протоколы XTLS, включая RPRX-Direct, Vision, REALITY
- Статистика трафика, лимит трафика, срок действия
- Настраиваемые шаблоны конфигурации Xray
- Поддерживает панель доступа HTTPS (самоутверждённое доменное имя + SSL-сертификат)
- Поддерживает приложение SSL-сертификата в один клик и автоматическое продление
- Для получения более продвинутых элементов конфигурации, пожалуйста, обратитесь к панели
- Исправлены маршруты API (пользовательские настройки будут созданы с помощью API)
- Поддерживает изменение конфигураций различными элементами, представленными на панели.
- Поддерживает базу данных экспорта/импорта из панели


## Настройки По Умолчанию

<details>
  <summary>Нажмите для получения подробной информации о настройках по умолчанию</summary>

  ### информация

- **Порт:** 2053
- **Имя пользователя и пароль:** Он будет сгенерирован случайным образом, если вы пропустите изменение.
- **Путь к базе данных:**
  - /etc/x-ui/x-ui.db
- **Путь Xray Config:**
  - /usr/local/x-ui/bin/config.json
- **Путь веб-панели б//o Развертывание SSL:**
  - http://ip:2053/panel
  - http://domain:2053/panel
- **Путь веб-панели с развертыванием SSL:**
  - https://domain:2053/panel
 
</details>

## [Конфигурация WARP](https://gitlab.com/fscarmen/warp)

<details>
  <summary>Нажмите для получения подробной информации о конфигурации WARP</summary>

#### Usage

If you want to use routing to WARP before v2.1.0 follow steps as below:

**1.** Install WARP on **SOCKS Proxy Mode**:

   ```sh
   bash <(curl -sSL https://raw.githubusercontent.com/hamid-gh98/x-ui-scripts/main/install_warp_proxy.sh)
   ```

**2.** If you already installed warp, you can uninstall using below command:

   ```sh
   warp u
   ```

**3.** Turn on the config you need in panel

   Config Features:

   - Block Ads
   - Route Google + Netflix + Spotify + OpenAI (ChatGPT) to WARP
   - Fix Google 403 error

</details>

## IP Limit

<details>
  <summary>Click for IP limit details</summary>

#### Usage

**Note:** IP Limit won't work correctly when using IP Tunnel

- For versions up to `v1.6.1`:

  - IP limit is built-in into the panel.

- For versions `v1.7.0` and newer:

  - To make IP Limit work properly, you need to install fail2ban and its required files by following these steps:

    1. Use the `x-ui` command inside the shell.
    2. Select `IP Limit Management`.
    3. Choose the appropriate options based on your needs.
   
  - make sure you have ./access.log on your Xray Configuration after v2.1.3 we have an option for it
  
  ```sh
    "log": {
      "access": "./access.log",
      "dnsLog": false,
      "loglevel": "warning"
    },
  ```

</details>

## Telegram Bot

<details>
  <summary>Click for Telegram bot details</summary>

#### Usage

The web panel supports daily traffic, panel login, database backup, system status, client info, and other notification and functions through the Telegram Bot. To use the bot, you need to set the bot-related parameters in the panel, including:

- Telegram Token
- Admin Chat ID(s)
- Notification Time (in cron syntax)
- Expiration Date Notification
- Traffic Cap Notification
- Database Backup
- CPU Load Notification


**Reference syntax:**

- `30 \* \* \* \* \*` - Notify at the 30s of each point
- `0 \*/10 \* \* \* \*` - Notify at the first second of each 10 minutes
- `@hourly` - Hourly notification
- `@daily` - Daily notification (00:00 in the morning)
- `@weekly` - weekly notification
- `@every 8h` - Notify every 8 hours

### Telegram Bot Features

- Report periodic
- Login notification
- CPU threshold notification
- Threshold for Expiration time and Traffic to report in advance
- Support client report menu if client's telegram username added to the user's configurations
- Support telegram traffic report searched with UUID (VMESS/VLESS) or Password (TROJAN) - anonymously
- Menu based bot
- Search client by email ( only admin )
- Check all inbounds
- Check server status
- Check depleted users
- Receive backup by request and in periodic reports
- Multi language bot

### Setting up Telegram bot

- Start [Botfather](https://t.me/BotFather) in your Telegram account:
    ![Botfather](./media/botfather.png)
  
- Create a new Bot using /newbot command: It will ask you 2 questions, A name and a username for your bot. Note that the username has to end with the word "bot".
    ![Create new bot](./media/newbot.png)

- Start the bot you've just created. You can find the link to your bot here.
    ![token](./media/token.png)

- Enter your panel and config Telegram bot settings like below:
![Panel Config](./media/panel-bot-config.png)

Enter your bot token in input field number 3.
Enter the user ID in input field number 4. The Telegram accounts with this id will be the bot admin. (You can enter more than one, Just separate them with ,)

- How to get Telegram user ID? Use this [bot](https://t.me/useridinfobot), Start the bot and it will give you the Telegram user ID.
![User ID](./media/user-id.png)

</details>

## API Routes

<details>
  <summary>Click for API routes details</summary>

#### Usage

- `/login` with `POST` user data: `{username: '', password: ''}` for login
- `/panel/api/inbounds` base for following actions:

| Method | Path                               | Action                                      |
| :----: | ---------------------------------- | ------------------------------------------- |
| `GET`  | `"/list"`                          | Get all inbounds                            |
| `GET`  | `"/get/:id"`                       | Get inbound with inbound.id                 |
| `GET`  | `"/getClientTraffics/:email"`      | Get Client Traffics with email              |
| `GET`  | `"/createbackup"`                  | Telegram bot sends backup to admins         |
| `POST` | `"/add"`                           | Add inbound                                 |
| `POST` | `"/del/:id"`                       | Delete Inbound                              |
| `POST` | `"/update/:id"`                    | Update Inbound                              |
| `POST` | `"/clientIps/:email"`              | Client Ip address                           |
| `POST` | `"/clearClientIps/:email"`         | Clear Client Ip address                     |
| `POST` | `"/addClient"`                     | Add Client to inbound                       |
| `POST` | `"/:id/delClient/:clientId"`       | Delete Client by clientId\*                 |
| `POST` | `"/updateClient/:clientId"`        | Update Client by clientId\*                 |
| `POST` | `"/:id/resetClientTraffic/:email"` | Reset Client's Traffic                      |
| `POST` | `"/resetAllTraffics"`              | Reset traffics of all inbounds              |
| `POST` | `"/resetAllClientTraffics/:id"`    | Reset traffics of all clients in an inbound |
| `POST` | `"/delDepletedClients/:id"`        | Delete inbound depleted clients (-1: all)   |
| `POST` | `"/onlines"`                       | Get Online users ( list of emails )       |

\*- The field `clientId` should be filled by:

- `client.id` for VMESS and VLESS
- `client.password` for TROJAN
- `client.email` for Shadowsocks


- [API Documentation](https://documenter.getpostman.com/view/16802678/2s9YkgD5jm)
- [<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://app.getpostman.com/run-collection/16802678-1a4c9270-ac77-40ed-959a-7aa56dc4a415?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D16802678-1a4c9270-ac77-40ed-959a-7aa56dc4a415%26entityType%3Dcollection%26workspaceId%3D2cd38c01-c851-4a15-a972-f181c23359d9)
</details>

## Environment Variables

<details>
  <summary>Click for environment variables details</summary>

#### Usage

| Variable       |                      Type                      | Default       |
| -------------- | :--------------------------------------------: | :------------ |
| XUI_LOG_LEVEL  | `"debug"` \| `"info"` \| `"warn"` \| `"error"` | `"info"`      |
| XUI_DEBUG      |                   `boolean`                    | `false`       |
| XUI_BIN_FOLDER |                    `string`                    | `"bin"`       |
| XUI_DB_FOLDER  |                    `string`                    | `"/etc/x-ui"` |
| XUI_LOG_FOLDER |                    `string`                    | `"/var/log"`  |

Example:

```sh
XUI_BIN_FOLDER="bin" XUI_DB_FOLDER="/etc/x-ui" go build main.go
```

</details>

## Preview

![1](./media/1.png)
![2](./media/2.png)
![3](./media/3.png)
![4](./media/4.png)
![5](./media/5.png)
![6](./media/6.png)
![7](./media/7.png)

## Acknowledgment

- [Iran v2ray rules](https://github.com/chocolate4u/Iran-v2ray-rules) (License: **GPL-3.0**): _Enhanced v2ray/xray and v2ray/xray-clients routing rules with built-in Iranian domains and a focus on security and adblocking._
- [Vietnam Adblock rules](https://github.com/vuong2023/vn-v2ray-rules) (License: **GPL-3.0**): _A hosted domain hosted in Vietnam and blocklist with the most efficiency for Vietnamese._

