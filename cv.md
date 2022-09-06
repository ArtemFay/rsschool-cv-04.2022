

## [rsschool-cv](https://github.com/ArtemFay/rsschool-cv)

# Artem Fayzulov 
<img src="ava.jpg" alt="drawing" width="300"/>

### Contact information:

Phone: +7 (937) 271-34-34                                               
E-mail: psgl2007@gmail.com                                                
discord: ArtemFay(@ArtemFay)                                                 
[Telegram](https://t.me/Artem_fay) [GitHub](https://github.com/ArtemFay) [CodeWars](https://www.codewars.com/users/ArtemFay)

***

### Briefly About Myself:
text About Myself

***

### Skills and Proficiency:
- GIT, GitHub
- Windows, MacOS 
- JavaScript, Google Apps Script
- HTML5, CSS3
- VS Code, terminal

***

### Code example:
> Kata from [CodeWars](https://www.codewars.com/) by [ArtemFay](https://www.codewars.com/users/ArtemFay)
>Trolls are attacking your comment section!
>A common way to deal with this situation is to remove all of the vowels from the trolls' comments, neutralizing the threat.
>Your task is to write a function that takes a string and return a new string with all vowels removed.
>For example, the string "This website is for losers LOL!" would become "Ths wbst s fr lsrs LL!".
>Note: for this kata y isn't considered a vowel.

My solution:
```js
const ss = SpreadsheetApp.getActive()
const raschet = ss.getSheetByName('📐 РАСЧЕТ')
const smetaSettings = ss.getSheetByName('Смета (настройка)')
const smeta = ss.getSheetByName('Смета')
const dataBase = ss.getSheetByName('БД')
const aSheetName = ss.getActiveSheet().getName()
const aRange = ss.getActiveRange()
const aA1 = aRange.getA1Notation()
const aVal = aRange.getValue()
const aCol = aRange.getColumn()

const arrayRaschet = [
  /* 
  [ Name, Coordinate in calculation, Coordinate in DB]
  */
  ['Тип скважины', 'B1', 'C'],
  ['Цена фильтра', 'B2', 'D'],
  ['Метр бурения ', 'B3', 'E'],
  ['Глубина скважины', 'B4', 'F'],
  ['Загрузка вручную', 'B5', 'G'],
  ['Скидка руб.', 'B6', 'H'],
  ['Коэфф. наценки', 'B7', 'I'],
  ['Обустройство', 'E2', 'J'],
  ['Насос', 'E3', 'K'],
  ['Гидробак', 'E7', 'L'],
  ['Автоматика', 'E9', 'M'],
  ['Термоусадка', 'E12', 'N'],
  ['3 ПНД муфты', 'E13', 'O'],
  ['4 зажима тросовых', 'E14', 'P'],
  ['Обратный клапан', 'E16', 'Q'],
  ['Сбросной клапан', 'E17', 'R'],
  ['Летний полив', 'E18', 'S'],
  ['Выходов из кессона', 'E19', 'T'],
  ['Греющий кабель', 'E20', 'U'],
  ['Траншея', 'E23', 'V'],
  ['Монтажные работы', 'E24', 'W'],
  ['Транспортные расходы', 'E25', 'X'],
  ['Стоимость доп. метров траншеи', 'E27', 'Y'],
  ['Подключение к системе', 'E30', 'Z'],
  ['Заведение за фундамент', 'E31', 'AA'],
  ['Пескобетон', 'E32', 'AB'],
]
}

function onEdit() {
// Autostart trigger. Contains the trigger conditions for each function. 
  if (aSheetName == '📐 РАСЧЕТ') {
    if (aA1 == 'E2') {
      defaultRaschet()
      if (aVal.toString().includes('Адаптер') || aVal.toString().includes('автоматикой')) { raschet.getRange('E17').setValue(1) }
      if (aVal.toString().includes('кессон')) { raschet.getRange('E17').setValue(0) }
    }

    if (aRange.isChecked()) {
      if (aA1 == 'K5') { saveRaschet() }
      if (aA1 == 'K1') { defaultRaschet(); Browser.msgBox('Расчет сброшен') }
      if (aCol == 11 && aRange.getRow() > 5) { loadRaschet() }
    }

    if (aA1 == 'E7' && aVal.toString().includes('ДЖИЛЕКС')) { raschet.getRange('E9').setValue('Нет') }
  }

  if (aSheetName == 'Смета (настройка)') {
    if (aCol == 9 && aRange.isChecked()) { aRange.offset(0, 1, 1, 6).setValue(true) }
    if (aCol == 9 && !aRange.isChecked()) { aRange.offset(0, 1, 1, 6).setValue(false) }
  }
}

function smetaGenerator() {
  // insert rows if there are less than 111
  if (smeta.getMaxRows() < 111) { smeta.insertRowsBefore(smeta.getMaxRows(), 111 - smeta.getMaxRows()) }
  // copy the entire estimate and format
  smeta.getRange('A1:F').clearContent().clearFormat()
  smetaSettings.getRange('A1:F').copyTo(smeta.getRange('A1:F'), SpreadsheetApp.CopyPasteType.PASTE_VALUES, false)
  smetaSettings.getRange('A1:F').copyTo(smeta.getRange('A1:F'), SpreadsheetApp.CopyPasteType.PASTE_FORMAT, false)
  // delete rows that are not needed for the selected type of arrangement (checkmarks)
  const obustrystvo = raschet.getRange('E2').getValue()
  const tipSmetyColumnsArray = [
    ['Металл. кессон', 10],
    ['Пластик. кессон Земляк', 10],
    ['Пластик. кессон ЭКОБАТ', 10],
    ['Пластик. кессон БИО-С', 10],
    ['Пластик кессон увелич. 1,2м*2м', 10],
    ['Пластик кессон long 1,2м*2,5м', 10],
    ['Пластик кессон увелич. 1,5м*2м', 10],
    ['Пластик кессон long 1,5м*2,5м', 10],
    ['Адаптер с гидробаком', 11],
    ['Адаптер без гидробака', 12],
    ['Летний полив', 13],
    ['Летний полив с автоматикой', 14],
    ['Металл. кессон (квадр. 1.2м)', 10],
    ['Металл. кессон (кругл. 1.2м)', 10],
    ['Металл. кессон (квадр. 1.5м)', 10],
    ['Металл. кессон (кругл. 1.5м)', 10],
    ['Погреб 1', 15],
    ['Погреб 2', 15],
    ['Погреб 3', 15],
  ]
  const numColl = tipSmetyColumnsArray.find(el => el[0] == obustrystvo)[1]
  const flags = smetaSettings.getRange(1, numColl, 111, 1).getValues()
  const stoimost = smetaSettings.getRange(1, 6, 111, 1).getValues()
  let rowsToDelite = []
  if (smetaSettings.getRange('D81').getValue() == 0) { rowsToDelite.push(81) }
  flags.forEach((el, i) => {
    if (el.toString() == 'false' || stoimost[i][0].toString() == '0') { rowsToDelite.push(i + 1) }
  })
  rowsToDelite.sort((a, b) => b - a).forEach(el => smeta.deleteRow(el))
  aRange.uncheck()
  Browser.msgBox('Расчет сохранен. Смета сформирована')
}

function defaultRaschet() {
  raschet.getRange('E32').setValue("С клиента")
  raschet.getRange('F32').setValue(0)
  raschet.getRange('E7').setValue('100 л')
  raschet.getRange('E9').setValue('AQUARIO')
  raschet.getRange('E19').setValue(1)
  raschet.getRange('E23').setValue(0)
  raschet.getRange('E20').setValue('Не нужен')
  raschet.getRange('B6').setValue(0)
  raschet.getRange('B7').setValue(1)
  aRange.uncheck()
}

  // functions for managing the saving and loading of calculations in the database
function saveRaschet() {
  let name = Browser.inputBox('SAVE', 'Enter link', Browser.Buttons.OK_CANCEL)
  if (name == 'cancel') { aRange.uncheck(); return }
  raschet.getRange('I6:J31').copyTo(raschet.getRange('I7'))
  raschet.getRange('I6:J6').clearContent().setValues([[new Date().toLocaleDateString('ru'), name]])
  let dataRaschet = [name, new Date().toLocaleDateString('ru')]
  arrayRaschet.forEach(el => { dataRaschet.push(raschet.getRange(el[1]).getValue()) })
  dataBase.deleteRow(32)
  dataBase.insertRowBefore(2)
  dataBase.getRange(2, 1, 1, dataRaschet.length).setValues([dataRaschet])
  smetaGenerator()
}
function loadRaschet() {
  let id = aRange.offset(0, -1).getValue()
  if (!id) { aRange.uncheck(); return }
  const idArray = dataBase.getRange('A1:A' + dataBase.getLastRow()).getValues().flat()
  let row = idArray.indexOf(id) + 1
  let dataRaschet = dataBase.getRange(row, 3, 1, arrayRaschet.length).getValues().flat()
  arrayRaschet.forEach((el, i) => { raschet.getRange(el[1]).setValue(dataRaschet[i]) })
  aRange.uncheck()
  Browser.msgBox('Расчет загружен')
}
```
***
<img src="smeta.jpg" alt="smeta" width="600"/>
### Experience:
[rsschool-cv](https://github.com/ArtemFay/rsschool-cv) - First project in RS-School.                          
[GitHub](https://github.com/ArtemFay) - My personal GitHub account with all of my projects.

***

### Languages:

English - pre-intermediate                          
Russian - native
