# MVP

1 ==> // Start 

2 ==> // Export Excel Sheets from Google Drive

Constant ExcelSheet1 = load_workbook(Sample1.csv, use_iterators=True)
Constant ExcelSheet2 = load_workbook(Sample2.csv, use_iterators=True)

3 ==> // Parse Excel Sheets into the Targated Row/Col

Constant sheet1 = ExcelSheet1.worksheets[0]
Constant sheet2 = ExcelSheet2.worksheets[0]
Constant Text1 = sheet[4]
Constant Text2 = sheet2[4]

4 ==> // Remove Syncategrmatic Words

def removearticles(Text1):
  re.sub('(\s+)(a|an|and|the)(\s+)', '\1\3', Text1)
  
def removearticles(Text2):
  re.sub('(\s+)(a|an|and|the)(\s+)', '\1\3', Text2)  

5 ==> // Break String into Words/Char

Constant Text1List = Text1.split()
Constant Text2List = Text2.split()

6 ==> // Spell Check from Google Pspell Library 

from spellchecker import SpellChecker
spell = SpellChecker()
spell.candidates(Text1List) // Auto Looping
spell.candidates(Text2List) // Auto Looping

7 ==> // Compare Char/Words to Generate Logics

For Text1List as List
  Constant counts[] = similar_text(Text1List[List],Text2List[List])
Endfor

8 ==> // Calculating Probability

Constant Probability = SUM(counts[])/count(Text1List) * 100

9 ==> // Display into the Targeted Excel Col

sheet2[4] = Probability

10 ==> // Save logs for Future Perceptions 
