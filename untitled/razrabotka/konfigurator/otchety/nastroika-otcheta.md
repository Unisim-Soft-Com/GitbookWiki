# Настройка отчета

**title** - выводится информация из SqlHeader

**title | Page** - на каждой странице

**title | General** - только на ПЕРВОЙ странице

**detail1** - выводится информация из SqlMaster

**summary** - подвал, для итога : \_\_поле

**params | JoinFields | поле группировки (без \_ )** - группировка по полю, без повторений, т.е. пишется один раз значение поля группировки

**groupF | \_поле группировки | PageBreak** - переход на новую страницу

**title | Page** - на каждой странице

**Все настраиваемые параметры страницы применяются после закрытия формы отчета в клиенте.**

Свойство **TXTFixedPreview=true** - отображает отчет в текстовом виде (н-р: заявка)

### [Direct link to heading](nastroika-otcheta.md#h42143e43743443043d43843543e44244743544243044144843043143b43e43d43e43c44243843f4302a.fr3) Создание отчета с шаблоном типа \*.fr3

Ссылка на пример отчета (файл находится в папке Настройка отчета):

[https://doc-08-bo-docs.googleusercontent.com/docs/securesc/9epombkml4j5pmvm41inf8g77qjjt8kp/rnqonq784kp9g46tg1vgnj36cmj1tqrg/1345471200000/05897270490584079318/05897270490584079318/0B4pVn7iLUWb2YUkwTmRyNkVQenc?e=download\&nonce=e3tvmqpmumrhs\&user=05897270490584079318\&hash=qnqsh1mdgcvhj09g14egnrfokt14uei2](https://doc-08-bo-docs.googleusercontent.com/docs/securesc/9epombkml4j5pmvm41inf8g77qjjt8kp/rnqonq784kp9g46tg1vgnj36cmj1tqrg/1345471200000/05897270490584079318/05897270490584079318/0B4pVn7iLUWb2YUkwTmRyNkVQenc?e=download\&nonce=e3tvmqpmumrhs\&user=05897270490584079318\&hash=qnqsh1mdgcvhj09g14egnrfokt14uei2)

Для отчетов с шаблоном **\*.fr3** необходимым свойством является:

**VersionFR=4**

Чтобы настроить **DataSet** шаблона нужно создать ПФ в документе с таким же SQL и шаблоном (в пф должно быть свойство **VersionFR=4**) и при печати этой ПФ нажать кнопку шаблон. Там можно настроить **DataSet** и поля отчета.

Свойство шаблона, которое отвечает за количество столбцов отчета:

**Columns=2**

Чтобы указать **DataSet** - пункт меню **Report - Data**.

Переменные в шаблоне должны иметь тот же **DataSet**, который был выбран для шаблона.

[PreviousУниверсальный отчет (УО)](universalnyi-otchet-uo.md) [NextКонвертировать frf в fr3](konvertirovat-frf-v-fr3.md)

Last updated 1 year ago
