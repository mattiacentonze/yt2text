# yt2text

Semplice e veloce script Bash per estrarre trascrizioni e sottotitoli da video YouTube in **testo piano pulito** o in formato **VTT con timestamp**.

Supporta il download dei sottotitoli manuali e generati automaticamente (con deduplicazione intelligente delle righe ripetute tipiche di YouTube), cache automatica dell'eseguibile `yt-dlp` e supporto per stdout (`-o -`).

## Prerequisiti

Lo script richiede solo utility standard disponibili su qualsiasi distribuzione Linux moderna:
- **Bash** (4+)
- **curl**
- **Python 3** (per il parsing e la pulizia del formato VTT)

Non richiede pacchetti Python di terze parti. L'estrattore `yt-dlp` aggiornato viene scaricato automaticamente alla prima esecuzione e memorizzato nella cache dell'utente (`~/.cache/yt2text/`).

## Installazione

```bash
git clone https://github.com/mattiacentonze/yt2text.git
cd yt2text
chmod +x yt2text
ln -s "$(pwd)/yt2text" ~/.local/bin/yt2text
# Opzionale: crea un alias breve yt2txt
ln -s "$(pwd)/yt2text" ~/.local/bin/yt2txt
```

## Utilizzo

```bash
# Estrae la trascrizione in testo pulito (default lingua italiana, fallback inglese)
yt2text -u "https://www.youtube.com/watch?v=VIDEO_ID" -o trascrizione.txt

# Stampa direttamente il testo a terminale (stdout)
yt2text -u "https://www.youtube.com/watch?v=VIDEO_ID" -o -

# Mantiene i timestamp nel formato originale WebVTT
yt2text -u "https://www.youtube.com/watch?v=VIDEO_ID" -o sottotitoli.vtt -t

# Specifica una lingua diversa (es. spagnolo 'es', francese 'fr')
yt2text -u "https://www.youtube.com/watch?v=VIDEO_ID" -o testo.txt -l es

# Aggiorna il motore yt-dlp memorizzato nella cache
yt2text -U -u "https://www.youtube.com/watch?v=VIDEO_ID" -o test.txt
```

### Opzioni

| Opzione | Descrizione |
|---|---|
| `-u URL` | **Obbligatorio.** URL del video YouTube |
| `-o FILE` | **Obbligatorio.** File di output desiderato, oppure `-` per stdout |
| `-l LANG` | Lingua preferita dei sottotitoli (default: `it`, fallback automatico a `en`) |
| `-t` | Mantiene i timestamp salvando il file in formato WebVTT |
| `-U` | Forza l'aggiornamento dell'eseguibile `yt-dlp` nella cache locale |
| `-h` | Mostra la guida all'uso |

## Licenza

Rilasciato sotto licenza [MIT](LICENSE).
