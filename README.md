# Regex-for-thesis
Tested in https://regex101.com/

## Figure (1)
`\b((?i)figure(s)?|fig\.)\s?([a-zA-Z]){0,4}(?:[IVXLCDM]+|\d+)(?:(?:[–\d\s,]*(?:and\s)?[–\d\s,]*)|(?:[–\d\s,]*(?:and\s)?[–\d\s,]*[a-zA-Z\d]+\s*,\s*)+[a-zA-Z\d]+\s+and\s+[a-zA-Z\d]+\s*)?(\.)?\b`

- Test cases
```
# ordinary cases
figure 1. blah blah
fig. 1 blah blah
figure 123456789. blah blah
Figure S2. blah blah
Fig. S123. blah blah

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
'in Figures 2 and 3, and Table 2. blah' 
blah (Fig. 1a, 1b and 1c, Tables S1 and Tables S2).blah
Figures 1a,1b and 2d blah

# It doesn't cover below:
Fig. S2B,C blah
fig. 2E blah
figure S2B,C blah
Figure 2E blah
controls (figure 3B). At 18 mo
controls (fig. 3B,C). At 18 mo
(figure 1; table 1).
(figure 2; p=3·95×10−21).
line (figure 3A), with 
trols (θ; see figure 3D legend).
ed Data Fig. 5) for
ed TJ (Fig.2E), it 
```
## Figure (2)
`(?i)(?:fig\.|figure)\s?[S\d]+[A-Z,]*(?=\s|\.|\b|$)`

- Test cases
```
Fig. S2B,C blah
fig. 2E blah
figure S2B,C blah
Figure 2E blah
controls (figure 3B). At 18 mo
controls (fig. 3B,C). At 18 mo
(figure 1; table 1).
(figure 2; p=3·95×10−21).
line (figure 3A), with 
trols (θ; see figure 3D legend).
ed Data Fig. 5) for
ed TJ (Fig.2E), it 
```

## Table (1)
`\b(?i)table(s)?\s?([a-zA-Z]){0,4}(?:[IVXLCDM]+|\d+)(?:(?:[–\d\s,]*(?:and\s)?[–\d\s,]*)|(?:[–\d\s,]*(?:and\s)?[–\d\s,]*[a-zA-Z\d]+\s*,\s*)+[a-zA-Z\d]+\s+and\s+[a-zA-Z\d]+\s*)?(\.)?\b`

- Test cases
```
# ordinary cases
table 1. blah blah
table 1 blah blah
table 123456789. blah blah
Table S2. blah blah
Table S123. blah blah

# anomalies
Table123 blah blah # no comma
table1 in blah blah # no space
table STaa1 blah blah

# Roman numerals
table I is
table VI is
table X is

# should not transform in this case
'table in' -> 'table in'
'table is blah blah' -> 'table is blah blah'

# Additional cases
'blah Table 1–2' -> 'blah {TABLE}'
'Table 1 and 2' -> '{TABLE}'
'in Tables 2 and 3, and Table 2. blah' 
blah (Table 1a, 1b and 1c, Tables S1 and Tables S2).blah
Tables 1a,1b and 2d blah

# It doesn't cover below:
Table S2B,C blah
table 2E blah
table S2B,C blah
Table 2E blah
controls (table 3B). At 18 mo
controls (table 3B,C). At 18 mo
line (table 3A), with 
trols (θ; see table 3D legend).
ed TJ (Table2E), it

```
## Table (2)
`(?i)(?:table)\s?[S\d]+[A-Z,]*(?=\s|\.|\b|$)`

- Test cases
```
Table S2B,C blah
table 2E blah
table S2B,C blah
Table 2E blah
controls (table 3B). At 18 mo
controls (table 3B,C). At 18 mo
line (table 3A), with 
trols (θ; see table 3D legend).
ed TJ (Table2E), it
```

future work:
in Fig. 1D2-4. P
pd (Fig. 2D3). 
(Fig. 1B2,3) and
...
