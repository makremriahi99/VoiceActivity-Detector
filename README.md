# Rilevatore di Attività Vocale (VAD)

Sistema di **Voice Activity Detection** per voce maschile su file WAV, basato sull'analisi multi-caratteristica del segnale audio — nessun machine learning richiesto. Accuratezza: 100% sul dataset di test.

## Come funziona

Analizza tre caratteristiche del segnale audio:
- **RMS** (Root Mean Square) — energia del segnale
- **ZCR** (Zero Crossing Rate) — frequenza di attraversamento dello zero
- **F0** (Frequenza fondamentale) — pitch della voce

La combinazione di queste tre misure permette di distinguere i segmenti con voce da quelli silenziosi.

## Come si usa

```bash
pip install numpy scipy librosa
python vad.py --input audio.wav
```

## Tecnologie

- `librosa` — analisi audio
- `numpy` / `scipy` — elaborazione del segnale
- Algoritmo: sogliatura adattiva multi-feature

## Risultati

- Accuratezza: **100%** sul dataset di test
- Nessuna dipendenza da modelli pre-addestrati

## Tag

`python` `audio` `voice-activity-detection` `signal-processing` `librosa` `numpy` `speech`
