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
Fig. 2E blah
Figure S2B,C blah
Figure 2E blah
```
## Figure (2)
`(?:Fig\.|Figure)\s+[S\d]+[A-Z,]+,?(?=\s+\w+)`

- Test cases
```
Fig. S2B,C blah
Fig. 2E blah
Figure S2B,C blah
Figure 2E blah
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
Table 2E blah
table S2B,C blah
Table 2E blah
```
## Table (2)
`(?:(?i)table)\s+[S\d]+[A-Z,]+,?(?=\s+\w+)`

- Test cases
```
Table S2B,C blah
Table 2E blah
table S2B,C blah
Table 2E blah
```


(?:(?i)table)\s+[S\d]+[A-Z,]+,?(?=\s+\w+)
