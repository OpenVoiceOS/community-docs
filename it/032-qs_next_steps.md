# Avvio rapido di OpenVoiceOS - Passaggi successivi

## Wow! Hai un dispositivo OVOS funzionante! E ora?

Le immagini predefinite sono dotate di un set predefinito di competenze installate, tra cui, ma non solo, data/ora e meteo. Provale.

Pronuncia questi comandi e goditi il risultato:

`Hey Mycroft, che ore sono?`

`Hey Mycroft, che giorno è oggi?`

`Hey Mycroft, qual è il meteo oggi?`

`Hey Mycroft, pioverà oggi?`

Sebbene siano installate diverse competenze predefinite, ce ne sono molte altre disponibili per essere utilizzate. Il link sottostante ti mostrerà come trovare e installare altre competenze.

[Installazione delle competenze](080-ht_skills.md)

Ma aspetta, c'è di più!

OVOS è altamente configurabile e utilizza un file in formato `JSON` o `YAML` per fornire queste opzioni. Mentre nella maggior parte dei casi OVOS dovrebbe semplicemente funzionare, a volte si deve o si vuole modificare alcune opzioni.

[Configurazione di OVOS](060-config.md)

OVOS viene fornito con un motore TTS (Text to Speech, dal testo al parlato) predefinito che parla con la voce originale `Alan-Pope` usata da Mycroft. Ce ne sono MOLTE altre tra cui scegliere. Il seguente link ti aiuterà a scegliere e configurare una voce diversa per il tuo assistente.

[Configurazione del motore TTS](090-ht_tts.md)

Il tuo dispositivo non capisce la tua voce quando parli? Esistono anche opzioni per diversi motori STT (Speech To Text, dal parlato al testo). Alcuni funzionano meglio di altri ma possono garantire meno privacy.

[Modifica del motore STT](102-ht_stt.md)

Il tuo assistente OVOS usa una parola di attivazione ("wake word") che gli fa sapere che è ora di iniziare ad ascoltare i tuoi comandi. Come valore predefinito, la frase per attivare OVOS è `Hey Mycroft`. Questa, come la maggior parte delle cose in OVOS, è totalmente configurabile. Segui il link per saperne di più.

[Cambiare la parola di attivazione](104-ht_ww.md)

I plugin PHAL consentono a OVOS di interagire con l'hardware e il sistema operativo sottostanti. Sono disponibili diversi plugin che possono essere installati ed eseguiti insieme.

[Configurazione dei plugin PHAL](110-ht_phal.md)

OVOS viene fornito con servizi predefiniti disponibili al pubblico. Questi includono server TTS e STT pubblici, un'API meteo fornita da [OpenMeteo](https://openmeteo.com/) , accesso a Wolfram e altro. Poiché OVOS è un sistema aperto e privato, puoi anche modificarli in base alle tue preferenze.

[Installa i tuoi servizi](999-not-implemented) **Lavori in corso**

## Interazione tramite riga di comando

Sebbene OVOS sia principalmente una piattaforma guidata dalla voce, a volte ha senso interagire tramite riga di comando (CLI) per la risoluzione dei problemi, i test o lo sviluppo. OVOS distribuisce diversi strumenti con [ovos-bus-client](https://github.com/OpenVoiceOS/ovos-bus-client) nella maggior parte delle distribuzioni.

### ovos-listen

Digitando il comando `ovos-listen` il servizio listener inizierà ad ascoltare i comandi vocali. Se non hai impostato una parola di attivazione o hai problemi con essa, questo può essere un buon modo per controllare se l'intero listener non funziona.

### ovos-speak

Il comando `ovos-speak` dirà all'assistente di dire qualsiasi cosa tu digiti dopo. Questo comando può essere utile per dimostrazioni o per fare scherzi a familiari o coinquilini nelle vicinanze. Ad esempio:

```bash
$ ovos-speak "Guarda mammina, nessun dato viene condiviso con le grandi compagnie!"
```

Nota le virgolette: devi includerle, altrimenti l'assistente dirà solo "Guarda".

### ovos-say-to

Il comando `ovos-say-to` invierà un'espressione all'assistente, che la elaborerà normalmente. In pratica salta la parte dell'interazione dal parlato al testo. Questo comando è utile in situazioni in cui non puoi o non vuoi parlare con l'assistente, ad esempio quando i coinquilini o i familiari stanno dormendo o quando stai già scrivendo per testare il codice di una nuova competenza.

Per esempio:

```bash
$ ovos-say-to "Che ore sono?"
```

Di nuovo, nota le virgolette. Senza virgolette solo la prima parola verrà inviata all'assistente, il che in genere darà luogo a un errore.
