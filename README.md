# Regex-for-thesis
Tested in https://regex101.com/

## Figure
`((?i)figure(s)?|fig\.)\s?([a-zA-Z]){0,4}(?:[IVXLCDM]+|\d+)(?:(?:[–\d\s,]*(?:and\s)?[–\d\s,]*)|(?:[–\d\s,]*(?:and\s)?[–\d\s,]*[a-zA-Z\d]+\s*,\s*)+[a-zA-Z\d]+\s+and\s+[a-zA-Z\d]+\s*)?(\.)?`

Test cases
```
# ordinary cases
figure 1. blah blah
fig. 1 blah blah
figure 123456789. blah blah
Figure S2. blah blah
Figure 123. blah blah

# anomalies
Figure123 blah blah # no comma
figure1 in blah blah # no space
figure STaa1 blah blah

# Roman numerals
figure I is
figure VI is
figure X is

# should not transform in this case
'figure in' -> 'figure in'
'figure is blah blah' -> 'figure is blah blah'

# Additional cases
'blah Figure 1–2' -> 'blah {FIGURE}'
'Figure 1 and 2' -> '{FIGURE}'
'in Figures 2 and 3, and Table 2. blah' -> 'in {FIGURE}, and Table 2. blah'
'blah (Fig. 1a, 1b and 1c, Tables S1 and Tables S2).blah' -> 'blah ({FIGURE}, Tables S1 and Tables S2).blah'
Figures 1a,1b and 2d
```

## Table
`(?i)table(s)?\s?([a-zA-Z]){0,4}(?:[IVXLCDM]+|\d+)(?:(?:[–\d\s,]*(?:and\s)?[–\d\s,]*)|(?:[–\d\s,]*(?:and\s)?[–\d\s,]*[a-zA-Z\d]+\s*,\s*)+[a-zA-Z\d]+\s+and\s+[a-zA-Z\d]+\s*)?(\.)?`
