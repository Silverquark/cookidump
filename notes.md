# Unicode fixing

The json output files has unencoded unicode strings in it: \u00be 

Get all unicode occurences and print the actual unicode char for each:

`grep -o -E '\\u....' data.json | sort --unique | while read line ; do printf '\n\\%s ' $line && printf "\\"$line ; done`

```
\u00a0 (NO-BREAK SPACE) - can be replaced with regular space
\u00ae ®
\u00b0 °
\u00b4 ´
\u00ba º
\u00bc ¼
\u00bd ½
\u00be ¾
\u00c4 Ä
\u00c7 Ç
\u00c9 É
\u00d6 Ö
\u00d8 Ø
\u00dc Ü
\u00df ß
\u00e0 à
\u00e1 á
\u00e2 â
\u00e4 ä
\u00e5 å
\u00e7 ç
\u00e8 è
\u00e9 é
\u00ea ê
\u00ed í
\u00ee î
\u00f1 ñ
\u00f6 ö
\u00fb û
\u00fc ü
\u011f ğ
\u0131 ı
\u0142 ł
\u015e Ş
\u015f ş
\u2013 –
\u201c “
\u201e „
\u2153 ⅓
\u2154 ⅔
\ue001 - kneading symbol
\ue002 - stir symbol
\ue003 - rotate symbol
\ue00c - heat symbol
\ue011 - fan symbol
\ue018 - xxx symbol
\ue01e - xxx symbol
\ue026 - xxx symbol
\ue02d - xxx symbol
\ue02e - xxx symbol
\ue031 - xxx symbol
```


Finding and replacing everything at once (this should have probably been a proper script...):

`grep -o -E '\\u....' data.json | sort --unique | while read line ; do printf '\n\\%s ' $line && printf "\\"$line ; done | while read line; do awk '{print "sed -i '\''s/\\"$1"/"$2"/g'\'' data.json" }' | bash; done;`
