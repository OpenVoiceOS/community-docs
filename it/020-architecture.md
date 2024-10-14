# Architettura di OpenVoiceOS

**Questa sezione può essere un po' tecnica ma è inclusa come riferimento.** Non è necessario leggere questa sezione per l'uso quotidiano di OVOS.

OVOS è una raccolta di servizi modulari che lavorano insieme per fornire un assistente vocale open source, riservato e fluido.

Il modo suggerito per avviare OVOS è con i file di servizio systemd. La maggior parte delle immagini esegue questi servizi come `user` (utente) normale anziché a livello di sistema. Se si verifica un errore quando si utilizzano i file di sistema, prova a utilizzarli come servizio di sistema.

**NOTA** `ovos.service` è solo un wrapper per controllare gli altri servizi OVOS. Viene qui utilizzato come esempio che mostra `--user` al posto di `system`.

- servizio utente
    - `systemctl --user status ovos.service`
- servizio di sistema
    - `systemctl status ovos.service`

## ovos-core

[ovos-core](https://github.com/OpenVoiceOS/ovos-core)

Questo servizio fornisce l'istanza principale di OVOS e gestisce il caricamento delle competenze e l'elaborazione degli intenti.

Tutte le domande degli utenti sono gestite dalle competenze (o "skill"). Puoi considerarle come il cervello di OVOS

tipico comando systemd

`systemctl --user status ovos-skills`

`systemctl --user restart ovos-skills`

[Documentazione tecnica sulle competenze](https://openvoiceos.github.io/ovos-technical-manual/skills_service/)

## Messagebus

[ovos-messagebus](https://github.com/OpenVoiceOS/ovos-messagebus)

Versione C++

**NOTA** Questa è una versione `alpha` e per lo più `un insieme di idee`. È noto che si blocca spesso.

[ovos-bus-service](https://github.com/OpenVoiceOS/ovos-bus_service)

Si può pensare al bus come al sistema nervoso di OVOS.

`ovos-bus` è considerato un websocket interno e privato, **i client esterni non dovrebbero connettersi direttamente ad esso. Si prega di non esporre il messagebus al mondo esterno!**

[Documentazione tecnica per messagebus](https://openvoiceos.github.io/ovos-technical-manual/bus_service/)

tipico comando systemd

`systemctl --user start ovos-messagebus`

## Listener

[ovos-dinkum-listener](https://github.com/OpenVoiceOS/ovos-dinkum-listener)

Il servizio listener è utilizzato per rilevare la tua voce. Controlla i plugin WakeWord, STT (Speech To Text) e VAD (Voice Activity Detection). Puoi modificare le impostazioni del microfono e abilitare funzionalità aggiuntive nella sezione listener del tuo file `mycroft.conf`, come ad esempio la registrazione e il caricamento della parola di attivazione o di intere espressioni.

[ovos-dinkum-listener](https://github.com/OpenVoiceOS/ovos-dinkum-listener) è il nuovo listener OVOS che ha sostituito l'originale [ovos-listener](https://github.com/OpenVoiceOS/ovos-listener) e ha molte più opzioni. Altri listener funzionano ancora ma non sono consigliati.

[Documentazione tecnica per i listener](https://openvoiceos.github.io/ovos-technical-manual/speech_service/)

tipico comando systemd

`systemctl --user start ovos-dinkum-listener`

### Plugin STT

Qui ciò che viene detto viene trascritto in testo e inoltrato al servizio delle competenze.

Possono essere caricati due plugin STT contemporaneamente. Se il plugin primario fallisce verrà utilizzato il secondo.

I modelli offline, avendo una precisione inferiore, come fallback tengono conto delle interruzioni di Internet, il che garantisce che il dispositivo non diventi mai completamente inutilizzabile.

Sono disponibili diversi plugin STT (Speech To Text). OVOS fornisce una serie di servizi pubblici tramite il plugin [ovos-stt-plugin-server](https://github.com/OpenVoiceOS/ovos-stt-plugin-server) ospitati da membri fidati di OVOS ([servizi di hosting dei membri](325-members.md#Members-hosting-services)). Non è richiesta alcuna configurazione aggiuntiva.

[Plugin STT supportati da OVOS](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-stt-plugin&type=all&language=&sort=)

[Come cambiare il plugin STT](102-ht_stt.md)

### Parole chiave

OVOS usa parole chiave (o "hotword") per innescare un numero qualsiasi di azioni. Puoi caricare un numero qualsiasi di parole chiave in parallelo e innescare azioni diverse quando vengono rilevate. Ogni parola chiave può fare una o più delle seguenti cose:

- attivare l'ascolto. Tale parola viene chiamata anche [parola di attivazione](#WakeWord-plugins) (o "wake word")
- riprodurre un suono
- emettere un evento bus
- togliere ovos-core dalla modalità di sospensione. Tale parola viene chiamata anche **wakeup_word** o **standup_word**
- togliere ovos-core dalla modalità di registrazione. Tale parola viene chiamata anche **stop_word**

[Impostazione e aggiunta di parole chiave](104-ht_ww.md)

#### Plugin WakeWord

Una parola d'attivazione (o "wake word") è ciò che OVOS usa per attivare il dispositivo. In maniera predefinita, `Hey Mycroft` è utilizzato da OVOS. Come altre cose nell'ecosistema OVOS, la parola d'attivazione è configurabile.

[Plugin per le parole di attivazione](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-ww-plugin&type=all&language=&sort=)

[Modifica della parola di attivazione](104-ht-ww.md)

### Plugin VAD

I plugin VAD rilevano quando stai effettivamente parlando con il dispositivo e quando smetti di parlare.

Nella maggior parte dei casi, non sarà necessario cambiare questo plugin. Se hai problemi con il microfono che ti sente o che non smette di ascoltare quando hai finito di parlare, potresti cambiarlo e vedere se ciò risolve il problema.

[Plugin VAD supportati](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-vad-plugin&type=all&language=&sort=)

[Modifica del plugin VAD](105-ht_vad.md)

## Audio

[ovos-audio](https://github.com/OpenVoiceOS/ovos-audio)

Il servizio audio gestisce l'output di tutto l'audio. È il modo in cui senti le risposte vocali, la musica o qualsiasi altro suono dal tuo dispositivo OVOS.

[Configurazione audio](999-not-implemented)

### Plugin TTS

TTS (Text To Speech) è la risposta verbale di OVOS. Sono disponibili diversi plugin che supportano diversi sistemi. Sono utilizzabili più lingue e più voci.

OVOS fornisce un set di server TTS pubblici ospitati da membri fidati di OVOS ([servizi di hosting dei membri](325-members.md#Members-hosting-services)). Utilizzando [ovos-tts-server-plugin](https://github.com/OpenVoiceOS/ovos-tts-server-plugin) non è necessaria alcuna configurazione aggiuntiva.

[Plugin TTS supportati](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-tts-plugin&type=all&language=&sort=)

[Modifica del plugin TTS](090-ht_tts.md)

## PHAL

[ovos-PHAL](https://github.com/OpenVoiceOS/ovos-PHAL)

PHAL sta per **Plugin-based Hardware Abstraction Layer**, "Layer di astrazione hardware basato su plugin". Viene utilizzato per consentire l'accesso di diversi dispositivi hardware per utilizzare lo stack software OVOS. Sostituisce completamente il concetto di "contenitore hardcoded" (cioè fissato nel codice) di `mycroft-core`.

È possibile caricare e convalidare in fase di esecuzione un numero qualsiasi di plugin che forniscono funzionalità. I plugin possono essere [integrazioni di sistema](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system), così da gestire operazioni come il riavvio e l'arresto, oppure driver hardware come [il plugin mycroft mark 1](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk1)

[Plugin PHAL supportati](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-phal-plugin&type=all&language=&sort=)

[Plugin PHAL](110-ht_phal.md)

### PHAL da amministratore

Simile al normale PHAL ma viene utilizzato quando è necessario `sudo` o un `utente privilegiato`. **Fai molta attenzione quando aggiungi i `plugin admin-phal`, dato che conferiscono privilegi amministrativi per OVOS o privilegi di root al tuo sistema operativo** [PHAL da amministratore](110-ht_phal.md#adimn-phal)

## Interfaccia grafica (GUI)

OVOS utilizza il framework standard mycroft-gui, per il quale puoi trovare la documentazione ufficiale [qui](https://mycroft-ai.gitbook.io/docs/skill-development/displaying-information/mycroft-gui)

Il servizio GUI fornisce un websocket a cui i client GUI possono connettersi ed è responsabile dell'implementazione del protocollo GUI in `ovos-core`.

Puoi trovare una documentazione approfondita [qui](https://openvoiceos.github.io/ovos-technical-manual/gui_service/)

## Altri servizi OVOS

OVOS fornisce una serie di script di supporto che consentono all'utente di controllare il dispositivo dalla riga di comando.

- `ovos-say-to` Questo fornisce un modo per comunicare un intento a OVOS.
- `ovos-say-to "che ore sono"`
- `ovos-listen` Questo apre il microfono per l'ascolto, proprio come se avessi detto la parola di attivazione. Si aspetta un comando verbale.
    - Continua dicendo al tuo dispositivo `"che ore sono"`
- `ovos-speak` Prende il tuo comando e lo esegue attraverso il motore TTS (Text To Speech) e pronuncia ciò che è stato fornito.
- `ovos-speak "ciao mondo"` produrrà `"ciao mondo"` nella voce TTS configurata
- `ovos-config` è un'interfaccia a riga di comando che consente di visualizzare e impostare i valori di configurazione.

**Solo per le immagini raspOVOS più recenti (&gt; nov 2023)**

- <code>docs-community</code> Visualizza la documentazione della comunità di OVOS nel terminale
- <code>docs-techincal</code> Visualizza la documentazione tecnica di OVOS nel terminale
- <code>docs-hivemind</code> Visualizza la documentazione di HiveMind nel terminale
- <code>docs-messages</code> Visualizza le specifiche dei messaggi di OVOS nel terminale
