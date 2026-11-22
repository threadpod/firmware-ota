# Vulnérabilités connues — project-threadpod-tpc 1.7.2242-202611221438

- Canal : `latest` — verdict : **conforme**
- Date : 2026-11-22T14:03:47Z
- NVD : NATIONAL VULNERABILITY DATABASE MIRROR (https://github.com/espressif/esp-nvd-mirror.git@0d1f7e3ed025fcc5dd8f704f569d808172fff691)
- OSV : 14 commits interrogés
- Registre des évaluations : `data/cra/vulnerabilites.yml`

## À évaluer (0)

Aucune.

## Évaluées par ThreadPod (9)

| vulnérabilité | composant | version | statut | justification | motif |
|---|---|---|---|---|---|
| CVE-2026-16554 | cJSON | 1.7.19 | non_affecte | vulnerable_code_not_present | print_string_ptr() et cJSON_PrintBuffered() sont rejetés à l'édition des liens ; il faudrait de plus environ 858 millions de caractères de contrôle, hors de la RAM du module |
| CVE-2026-67215 | cJSON | 1.7.19 | non_affecte | vulnerable_code_not_present | cJSONUtils_ApplyPatches() vit dans cJSON_Utils.c, qu'aucune archive liée ne contient |
| CVE-2026-67216 | cJSON | 1.7.19 | non_affecte | vulnerable_code_not_present | cJSON_Compare() n'est appelé par aucun code du binaire ; sa section est rejetée à l'édition des liens |
| CVE-2026-67217 | cJSON | 1.7.19 | non_affecte | vulnerable_code_not_present | apply_patch() vit dans cJSON_Utils.c, qu'aucune archive liée ne contient |
| CVE-2024-28115 | freertos | 10.5.1 | non_affecte | vulnerable_code_not_present | Vise les portages ARMv7-M MPU et ARMv8-M avec configENABLE_MPU=1 ; l'ESP32-C6 compile le seul portage portable/riscv, sans MPU wrappers (portUSING_MPU_WRAPPERS=0) |
| CVE-2026-77234 | freertos | 10.5.1 | non_affecte | vulnerable_code_cannot_be_controlled_by_adversary | Exige une tâche non privilégiée sous MPU wrappers ; portUSING_MPU_WRAPPERS=0 sur le portage RISC-V, et l'identifiant de commande des timers ne vient que des macros xTimer* du firmware |
| CVE-2026-77235 | freertos | 10.5.1 | non_affecte | vulnerable_code_not_present | SecureContext_FreeContext() vit dans le côté sécurisé des portages ARMv8-M TrustZone ; aucun fichier secure_context*.c n'est dans le composant freertos de l'IDF, l'ESP32-C6 compile portable/riscv |
| CVE-2026-77236 | freertos | 10.5.1 | non_affecte | vulnerable_code_not_present | SecureContext_AllocateContext() vit dans le côté sécurisé des portages ARMv8-M TrustZone ; aucun fichier secure_context*.c n'est dans le composant freertos de l'IDF, l'ESP32-C6 compile portable/riscv |
| CVE-2026-77237 | freertos | 10.5.1 | non_affecte | vulnerable_code_cannot_be_controlled_by_adversary | Exige une tâche non privilégiée sous MPU wrappers ; portUSING_MPU_WRAPPERS=0 sur le portage RISC-V, et ThreadPod OS n'appelle pas xQueueAddToSet, dont le handle ne vient que du firmware |

## Exclues par l'amont (10)

| vulnérabilité | composant | version | motif d'Espressif |
|---|---|---|---|
| CVE-2025-27840 | esp-idf | 6.0.2 | A security issue was reported concerning undocumented HCI commands in ESP32 Bluetooth controller. Espressif had earlier clarified that these vendor HCI commands are primarily used for debugging purposes and pose no real, known security threat. Technical details were shared in this https://developer.espressif.com/blog/2025/03/esp32-bluetooth-clearing-the-air/ |
| CVE-2020-22283 | lwip | 2.2.0 | ICMPv6 out-of-bounds read (savannah #58553) in icmp6_send_response_with_addrs_and_netif(). Fixed upstream by commits 489405839ae0 and 488d4ad2460c (lwIP 2.1.3/2.2.0), further hardened by 2bf8fcd7c240; all present as ancestors in the vendored esp-lwip fork. NVD's CPE has no fixed-version boundary ("git head"), causing the version match. |
| CVE-2026-15340 | lwip | 2.2.0 | Overflow of tx_buf in smtp_prepare_auth_or_mail() of the lwIP SMTP client application (src/apps/smtp/smtp.c) when a server sends an AUTH line longer than SMTP_TX_BUF_LEN, fixed upstream by 614420f82c87 (ICSA-26-279-02). The advisory lists 2.2.1, but 2.1.3 and 2.2.0 have the same code. ESP-IDF does not build src/apps/smtp/smtp.c. |
| CVE-2026-87121 | lwip | 2.2.0 | Out-of-bounds write into client->rx_buffer in mqtt_parse_incoming() of the lwIP MQTT client application (src/apps/mqtt/mqtt.c), fixed upstream by 68b2c1191886 (ICSA-26-265-01). ESP-IDF does not build src/apps/mqtt/mqtt.c. Its MQTT client is the separate ESP-MQTT component. |
| CVE-2026-91018 | lwip | 2.2.0 | Double free of the input pbuf in lowpan6_input() of the lwIP 6LoWPAN netif (src/netif/lowpan6.c) when decompression of a FRAG1 fragment fails, fixed upstream by f873b6295933 (ICSA-26-265-02). ESP-IDF does not build src/netif/lowpan6.c or src/netif/lowpan6_common.c. Thread support uses the 6LoWPAN layer of OpenThread. |
| CVE-2025-27810 | mbed_tls | 4.1.0 | Fixed in 3.6.3 |
| CVE-2025-52496 | mbed_tls | 4.1.0 | Fixed in 3.6.4 |
| CVE-2025-54764 | mbed_tls | 4.1.0 | Fixed in 3.6.5 |
| CVE-2025-59438 | mbed_tls | 4.1.0 | Fixed in 3.6.5 |
| CVE-2025-66442 | mbed_tls | 4.1.0 | Applicable only with Clang with select-optimize feature. ESP-IDF uses gcc as the default compiler and uses -Os as the default optimisation flag |

## Évaluations du registre que le scan ne trouve pas (33)

| vulnérabilité | composant | version | statut | motif |
|---|---|---|---|---|
| CVE-2026-113783 | esp-idf | 6.0.2 | non_affecte | Exposé seulement si CONFIG_LWIP_DNS_MAX_HOST_IP vaut 2 ou plus ; ThreadPod OS garde le défaut 1, la copie de dns_lookup() reste bornée à une entrée |
| CVE-2026-113782 | esp-idf | 6.0.2 | non_affecte | Exposé seulement avec CONFIG_OPENTHREAD_BORDER_ROUTER=y ; OpenThread est désactivé (Wi-Fi seul), le Border Router n'est pas compilé |
| CVE-2026-113780 | esp-idf | 6.0.2 | non_affecte | Plage affectée v6.0.3 à v6.0.4, avec ESP-TEE activé ; v6.0.2 est hors plage et CONFIG_SECURE_ENABLE_TEE n'est pas posé |
| CVE-2026-119086 | freertos | 10.5.1 | non_affecte | Exige une tâche non privilégiée sous MPU wrappers ; portUSING_MPU_WRAPPERS=0 sur le portage RISC-V, et ThreadPod OS n'appelle pas xQueueSelectFromSet, dont le handle ne vient que du firmware |
| CVE-2026-112062 | lwip | 2.2.0 | non_affecte | mdns_handle_response() vit dans src/apps/mdns/mdns.c, absent de la liste de sources du composant lwip de l'IDF v6.0.2 ; LWIP_MDNS_RESPONDER n'est pas posé |
| CVE-2026-119053 | lwip | 2.2.0 | non_affecte | snmp_pbuf_stream_writeto() vit dans src/apps/snmp/, absent de la liste de sources du composant lwip de l'IDF v6.0.2 ; LWIP_SNMP n'est pas posé |
| CVE-2026-8836 | lwip | 2.2.0 | non_affecte | snmp_parse_inbound_frame() vit dans src/apps/snmp/snmp_msg.c, absent de la liste de sources du composant lwip de l'IDF v6.0.2 ; LWIP_SNMP n'est pas posé |
| CVE-2026-115488 | mbed_tls | 4.1.0 | non_affecte | Exige MBEDTLS_SSL_VARIABLE_BUFFER_LENGTH et un serveur TLS ; CONFIG_MBEDTLS_SSL_VARIABLE_BUFFER_LENGTH n'est pas posé, handle_buffer_resizing() n'est pas compilé, et aucun serveur TLS n'est instancié |
| CVE-2026-115490 | mbed_tls | 4.1.0 | non_affecte | Exige MBEDTLS_SSL_PROTO_TLS1_2 et MBEDTLS_SSL_PROTO_TLS1_3 ensemble ; CONFIG_MBEDTLS_SSL_PROTO_TLS1_3 n'est pas posé, la machine d'état TLS 1.3 n'est pas compilée (mbedtls_ssl_tls13_handshake_client_step absent de l'ELF) |
| CVE-2026-115491 | mbed_tls | 4.1.0 | non_affecte | Serveur TLS 1.3 avec MBEDTLS_SSL_EARLY_DATA ; ni CONFIG_MBEDTLS_SSL_PROTO_TLS1_3 ni CONFIG_MBEDTLS_SSL_EARLY_DATA ne sont posés |
| CVE-2026-116375 | mbed_tls | 4.1.0 | non_affecte | Serveur TLS 1.3 avec rappel SNI ; CONFIG_MBEDTLS_SSL_PROTO_TLS1_3 n'est pas posé et mbedtls_ssl_conf_sni n'est pas lié |
| CVE-2026-50580 | mbed_tls | 4.1.0 | non_affecte | Client TLS 1.2 ECDHE-PSK ; CONFIG_MBEDTLS_PSK_MODES et CONFIG_MBEDTLS_KEY_EXCHANGE_ECDHE_PSK ne sont pas posés, MBEDTLS_KEY_EXCHANGE_ECDHE_PSK_ENABLED n'est pas défini et mbedtls_ssl_conf_psk n'est pas lié |
| CVE-2026-50581 | mbed_tls | 4.1.0 | non_affecte | MBEDTLS_PSA_ASSUME_EXCLUSIVE_BUFFERS est posé (esp_config.h:60), l'avis ne laisse donc que la perte d'unicité du secret maître, qui n'atteint qu'un protocole lié à ce secret ; aucun n'est au produit (ni EAP-TLS, ni export de clés : mbedtls_ssl_set_export_keys_cb absent de l'ELF) |
| CVE-2026-50586 | mbed_tls | 4.1.0 | non_affecte | Serveur TLS 1.2 émettant des tickets ; le seul appelant de mbedtls_ssl_config_defaults est le client esp-tls (MBEDTLS_SSL_IS_CLIENT), et mbedtls_ssl_conf_session_tickets_cb comme mbedtls_ssl_ticket_write sont absents de l'ELF |
| CVE-2026-50588 | mbed_tls | 4.1.0 | non_affecte | Exige MBEDTLS_KEY_EXCHANGE_ECJPAKE_ENABLED ; CONFIG_MBEDTLS_KEY_EXCHANGE_ECJPAKE n'est pas posé, la macro n'est pas définie |
| CVE-2026-50640 | mbed_tls | 4.1.0 | non_affecte | Serveur TLS 1.3 ; CONFIG_MBEDTLS_SSL_PROTO_TLS1_3 n'est pas posé |
| CVE-2026-73064 | mbed_tls | 4.1.0 | non_affecte | Serveur TLS 1.3 émettant des tickets ; CONFIG_MBEDTLS_SSL_PROTO_TLS1_3 n'est pas posé, l'avis exclut TLS 1.2 |
| CVE-2026-73096 | mbed_tls | 4.1.0 | non_affecte | Early data TLS 1.3 côté serveur ; ni CONFIG_MBEDTLS_SSL_PROTO_TLS1_3 ni CONFIG_MBEDTLS_SSL_EARLY_DATA ne sont posés |
| CVE-2026-90471 | mbed_tls | 4.1.0 | non_affecte | Ne contourne qu'une restriction de courbes posée par mbedtls_ssl_conf_groups() ; aucun code ne l'appelle (absent de l'ELF), les courbes admises sont celles de la configuration de build |
| CVE-2026-93776 | mbed_tls | 4.1.0 | non_affecte | Serveur TLS à hôtes virtuels par SNI ; aucun serveur TLS n'est instancié (seul set_client_config d'esp-tls appelle mbedtls_ssl_config_defaults) et ni mbedtls_ssl_conf_sni ni le cache de sessions ne sont liés |
| CVE-2026-93777 | mbed_tls | 4.1.0 | non_affecte | Serveur TLS 1.2 restreignant les signatures du client ; aucun serveur TLS n'est instancié et mbedtls_ssl_conf_sig_algs n'est pas lié |
| CVE-2026-93831 | mbed_tls | 4.1.0 | non_affecte | Serveur TLS 1.2 et 1.3 acceptant des tickets ; CONFIG_MBEDTLS_SSL_PROTO_TLS1_3 n'est pas posé, aucun ticket TLS 1.3 n'existe, et aucun serveur TLS n'est instancié |
| CVE-2026-93843 | mbed_tls | 4.1.0 | non_affecte | Mise en place d'un transform TLS 1.3 ; CONFIG_MBEDTLS_SSL_PROTO_TLS1_3 n'est pas posé |
| CVE-2026-93844 | mbed_tls | 4.1.0 | non_affecte | Exige MBEDTLS_SSL_VARIABLE_BUFFER_LENGTH ; CONFIG_MBEDTLS_SSL_VARIABLE_BUFFER_LENGTH n'est pas posé, handle_buffer_resizing() n'est pas compilé (les quatre autres conditions sont réunies : renégociation et MFL compilées et activées) |
| CVE-2025-27809 | mbed_tls | 4.1.0 | non_affecte | Plage relue à l'avis : Mbed TLS jusqu'à 3.6.2 ; 4.1.0 refuse la vérification sans nom (MBEDTLS_ERR_SSL_CERTIFICATE_VERIFICATION_WITHOUT_HOSTNAME, library/ssl_tls.c:8688), et esp-tls appelle mbedtls_ssl_set_hostname, skip_common_name n'étant jamais posé |
| MBEDTLS-2020-09-3 | mbed_tls | 4.1.0 | non_affecte | Vise l'échange DHE-PSK, retiré de Mbed TLS 4.0 (library/mbedtls_config_check_user.h:748, ChangeLog « Remove support for the DHE-PSK key exchange in TLS 1.2 ») |
| CVE-2026-115489 | mbed_tls | 4.1.0 | non_affecte | mbedtls_x509_dn_gets() n'est appelée par aucun code du binaire ; elle est absente de l'ELF |
| CVE-2026-49300 | mbed_tls | 4.1.0 | non_affecte | L'avis n'affecte qu'une application qui accepte un certificat directement d'un tiers non fiable ; le module n'accepte qu'une chaîne ancrée au bundle d'autorités ou à une ancre privée compilée, vérifiée par Mbed TLS lui-même, et n'enregistre aucune racine venue du réseau |
| CVE-2026-50579 | mbed_tls | 4.1.0 | non_affecte | mbedtls_pkcs7_free() n'est appelée par aucun code du binaire ; aucun symbole mbedtls_pkcs7_* n'est dans l'ELF |
| CVE-2026-90470 | mbed_tls | 4.1.0 | non_affecte | N'affecte qu'un nom attendu qui n'est pas un nom DNS ; le nom passé à mbedtls_ssl_set_hostname est toujours l'hôte d'une URL ou le common_name fixe de la box Overkiz, un nom DNS ou une adresse IP |
| CVE-2026-90475 | mbed_tls | 4.1.0 | non_affecte | L'ajout d'une CRL vit dans mbedtls_x509_crl_parse_der(), absente de l'ELF ; aucun symbole mbedtls_x509_crl_* n'est lié |
| MBEDTLS-2026-07-pkcs7-weak-hash-algorithms-accepted | mbed_tls | 4.1.0 | non_affecte | mbedtls_pkcs7_signed_data_verify() et mbedtls_pkcs7_signed_hash_verify() ne sont appelées par aucun code du binaire ; aucun symbole mbedtls_pkcs7_* n'est dans l'ELF |
| CVE-2026-116462 | mbed_tls | 4.1.0 | non_affecte | Ne joue qu'à la vérification d'une CRL ; aucune CRL n'est chargée (ni mbedtls_x509_crl_parse ni mbedtls_x509_crl_init dans l'ELF), et mbedtls_ssl_conf_ca_chain reçoit toujours une CRL nulle |

## Ce que le scan ne voit pas

La NVD est interrogée par CPE : 8 paquets sur 87 en portent un. Depuis le 15/04/2026, la NVD n'enrichit plus que les failles exploitées, fédérales ou critiques : une faille sans CPE rattaché n'y est pas trouvée. OSV est interrogé par commit pour les paquets épinglés par git.

- **Avec CPE** (8) : cJSON, component-chip, esp-idf, freertos, lwip, mbed_tls, micro-ecc, tf-psa-crypto
- **Commit seul, couverts par OSV seul** (73) : component-app_update, component-bootloader, component-bootloader_support, component-cxx, component-efuse, component-esp-tls, component-esp_app_format, component-esp_coex, component-esp_common, component-esp_driver_dma, component-esp_driver_gpio, component-esp_driver_i2c, component-esp_driver_rmt, component-esp_driver_spi, component-esp_driver_tsens, component-esp_driver_uart, component-esp_driver_usb_serial_jtag, component-esp_eth, component-esp_event, component-esp_hal_ana_conv, component-esp_hal_clock, component-esp_hal_dma, component-esp_hal_gpio, component-esp_hal_gpspi, component-esp_hal_i2c, component-esp_hal_mspi, component-esp_hal_pmu, component-esp_hal_rmt, component-esp_hal_security, component-esp_hal_uart, component-esp_hal_wdt, component-esp_http_client, component-esp_http_server, component-esp_hw_support, component-esp_matter, component-esp_mm, component-esp_netif, component-esp_partition, component-esp_phy, component-esp_pm, component-esp_ringbuf, component-esp_rom, component-esp_security, component-esp_stdio, component-esp_system, component-esp_timer, component-esp_wifi, component-espcoredump, component-espressif__cjson, component-espressif__led_strip, component-espressif__mdns, component-freertos, component-hal, component-heap, component-log, component-lwip, component-mbedtls, component-nvs_flash, component-nvs_sec_provider, component-partition_table, component-pthread, component-riscv, component-soc, component-spi_flash, component-tcp_transport, component-vfs, esp_libc, HTTP Parser, project-threadpod-tpc, submodule-esp_coex-lib, submodule-esp_phy-lib, submodule-esp_wifi-lib, submodule-heap-tlsf
- **Sans identifiant exploitable, non scannés** (6) : picolib, threadpod-hal, threadpod-mbedtls-crt-bundle, threadpod-os, threadpod-wpa-supplicant, toolchain-riscv32-esp-elf

## Composants retirés de la SBOM (98)

Non liés au binaire selon esp-idf-sbom et la map du build : Apache Mynewt Nimble, argtable3, component-app_trace, component-bt, component-cmock, component-console, component-driver, component-esp_adc, component-esp_blockdev, component-esp_blockdev_util, component-esp_bootloader_format, component-esp_driver_ana_cmpr, component-esp_driver_bitscrambler, component-esp_driver_cam, component-esp_driver_dac, component-esp_driver_gptimer, component-esp_driver_i2s, component-esp_driver_i3c, component-esp_driver_isp, component-esp_driver_jpeg, component-esp_driver_ledc, component-esp_driver_mcpwm, component-esp_driver_parlio, component-esp_driver_pcnt, component-esp_driver_ppa, component-esp_driver_sd_intf, component-esp_driver_sdio, component-esp_driver_sdm, component-esp_driver_sdmmc, component-esp_driver_sdspi, component-esp_driver_touch_sens, component-esp_driver_twai, component-esp_gdbstub, component-esp_hal_ana_cmpr, component-esp_hal_cam, component-esp_hal_i2s, component-esp_hal_ieee802154, component-esp_hal_jpeg, component-esp_hal_lcd, component-esp_hal_ledc, component-esp_hal_mcpwm, component-esp_hal_parlio, component-esp_hal_pcnt, component-esp_hal_ppa, component-esp_hal_rtc_timer, component-esp_hal_sd, component-esp_hal_timg, component-esp_hal_touch_sens, component-esp_hal_twai, component-esp_hal_usb, component-esp_hid, component-esp_https_ota, component-esp_https_server, component-esp_lcd, component-esp_local_ctrl, component-esp_matter_bridge, component-esp_matter_console, component-esp_matter_controller, component-esp_matter_ota_provider, component-esp_matter_rainmaker, component-esp_netif_stack, component-esp_psram, component-esp_tee, component-esp_trace, component-esp_usb_cdc_rom_console, component-espressif__esp_delta_ota, component-espressif__esp_encrypted_img, component-espressif__esp_secure_cert_mgr, component-esptool_py, component-idf_test, component-ieee802154, component-protobuf-c, component-protocomm, component-sdmmc, component-spiffs, component-ulp, component-unity, component-wear_levelling, FatFs, FreeRTOS-Plus-POSIX, openthread, openthread component, protobuf-c, submodule-bt-controller/lib_esp32, submodule-bt-controller/lib_esp32c2/esp32c2-bt-lib, submodule-bt-controller/lib_esp32c3_family, submodule-bt-controller/lib_esp32c5/esp32c5-bt-lib, submodule-bt-controller/lib_esp32c6/esp32c6-bt-lib, submodule-bt-controller/lib_esp32h2/esp32h2-bt-lib, submodule-bt-esp_ble_mesh/lib/lib, submodule-cmock-CMock, submodule-cmock-CMock-vendor/c_exception, submodule-cmock-CMock-vendor/unity, submodule-openthread-lib, submodule-openthread-openthread-third_party/mbedtls/repo, submodule-openthread-openthread-third_party/mbedtls/repo-framework, submodule-spiffs-spiffs, submodule-unity-unity

Gardés alors que l'outil les retirait :

| paquet | motif |
|---|---|
| component-bootloader | Le second étage de démarrage est livré dans l'image -full.bin, hors de la map de l'application |
| component-chip | lié au binaire : esp-idf/chip/lib/libCHIP.a dans la map |
| component-partition_table | La table de partitions est livrée dans l'image -full.bin, hors de la map de l'application |
| micro-ecc | porté par component-bootloader, gardé |
| threadpod-mbedtls-crt-bundle | composant ThreadPod (components/mbedtls_crt_bundle) : son code compile dans un autre composant |
