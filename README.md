# hse_hw1_meth

https://colab.research.google.com/drive/1EDGEaZTFvVUCvGZBlJ4qgd8Z-knqAnfk?usp=sharing

Есть 3 образца:

* 8cell – 8-клеточный эмбрион, примерно 2.25 дня после оплодотворения яйцеклетки

* ICM – внутренняя клеточная масса бластоциста, примерно 3.5 дня после оплодотворения яйцеклетки
 
* Epiblast – стадия эпибласта, примерно 6.5 дней после оплодотворения яйцеклетки

# Часть 1
Сравниваем fastqc report для BS-seq 8cell (слева) с fastqc report для RNA-seq SRR3414629_1 из прошлого дз3 (справа).
<p float="left">
  <img width="500" alt="Снимок экрана 2022-02-18 в 13 29 45" src="https://user-images.githubusercontent.com/91221560/154665566-bf42e934-69ed-44a2-852e-bc44b8da0458.png"> 
  <img width="500" alt="Снимок экрана 2022-02-18 в 13 34 23" src="https://user-images.githubusercontent.com/91221560/154666347-7b418687-787c-40d5-98ea-9e1fbf6cccf5.png">
</p>
* Видим, что у нашего запуска GC содержание меньше, оно составляет 36%, а у RNA-seq 49%. 
<p float="left">
  <img width="500" alt="Снимок экрана 2022-02-18 в 13 53 10" src="https://user-images.githubusercontent.com/91221560/154669359-186cdf5b-efe0-469c-a228-271794f5b757.png">
  <img width="500" alt="Снимок экрана 2022-02-18 в 13 53 40" src="https://user-images.githubusercontent.com/91221560/154669417-253488d1-fceb-4874-8143-06cbd7d78331.png">
 </p>
 * Per base sequence quality и Per sequence quality scores и там, и там в норме.
 <p float="left">
   <img width="500" alt="Снимок экрана 2022-02-18 в 14 05 22" src="https://user-images.githubusercontent.com/91221560/154671143-d5d50ed0-79d6-4bd8-b7a8-360c84120f04.png">
 <img width="500" alt="Снимок экрана 2022-02-18 в 14 09 10" src="https://user-images.githubusercontent.com/91221560/154671670-7d9f7841-e271-4d3a-a757-f5e3457d05cd.png">
 </p>
 <p float="left">
 <img width="500" alt="Снимок экрана 2022-02-18 в 14 11 02" src="https://user-images.githubusercontent.com/91221560/154672125-c6494476-09aa-427d-a3b0-3925a0d35fef.png">
<img width="500" alt="Снимок экрана 2022-02-18 в 14 11 31" src="https://user-images.githubusercontent.com/91221560/154673227-207460e4-eaa8-442c-b71d-d475909667f7.png">
 </p>
 * Per base sequence content сильно различаются, в нашем запуске 8cell большое содержание нуклеотида T и малое содержание C.
<p float="left">
 <img width="500" alt="Снимок экрана 2022-02-18 в 14 32 13" src="https://user-images.githubusercontent.com/91221560/154674932-820d7943-2a82-47ac-abfa-f68e8c375085.png">
 <img width="500" alt="Снимок экрана 2022-02-18 в 14 32 24" src="https://user-images.githubusercontent.com/91221560/154674958-8557310a-32c2-4d9c-b61b-347ec72ec928.png">
</p>
* Per sequence GC content у нашего запуска не в норме - сильно отличается от theoretical distribution, а у образца из предыдущего дз в норме.


# Часть 2

**Пункт (a)**

Работа с bam-files с выравниваниями BS-seq ридов на 11-ю хромосому мыши. 

Число ридов, закартированных на участки (1) 11347700-11367700; (2) 40185800-40195800 приведены в таблице:

<img width="363" alt="Снимок экрана 2022-02-18 в 14 43 17" src="https://user-images.githubusercontent.com/91221560/154677294-7570d8c8-7362-4610-a378-707aadb00645.png">

**bash-скрипт для дедупликации всех образцов одновременно**:

! ls *pe.bam | xargs -P 4 -tI{} deduplicate_bismark --bam --paired -o s_{} {}

Процент дуплицированных прочтений в каждом из образцов:

<img width="550" alt="Снимок экрана 2022-02-16 в 20 11 00" src="https://user-images.githubusercontent.com/91221560/154318812-f91a3191-36ec-4044-b8c9-0e3dc2f023f0.png">

**Пункт (b)**

Коллинг метилирования (см. в ноутбуке)

**Пункт (c)**

Из отчетов html:
<p float="left">
  <img width="300" alt="Снимок экрана 2022-02-18 в 15 05 34" src="https://user-images.githubusercontent.com/91221560/154679979-b5bb86a5-81f3-41b6-99b0-e6f03a8e57d2.png"> 
  <img width="300" alt="Снимок экрана 2022-02-18 в 15 05 43" src="https://user-images.githubusercontent.com/91221560/154679992-09ba3742-c3e8-49ed-aba1-e249ea9d9f93.png">
  <img width="300" alt="Снимок экрана 2022-02-18 в 15 05 52" src="https://user-images.githubusercontent.com/91221560/154680003-32c4cc7a-4849-4cbc-ad2b-cdc7deae5c64.png">
 </p>
 
 M-bias plots для Read1:
 <p float="left">
   <img width="300" alt="Снимок экрана 2022-02-18 в 15 09 53" src="https://user-images.githubusercontent.com/91221560/154680610-91c6558b-e605-4b3b-9823-f4c4a080786b.png">
  <img width="300" alt="Снимок экрана 2022-02-18 в 15 10 07" src="https://user-images.githubusercontent.com/91221560/154680617-3cbdc947-746e-4a89-af6a-e6ab61fc445d.png">
  <img width="300" alt="Снимок экрана 2022-02-18 в 15 10 26" src="https://user-images.githubusercontent.com/91221560/154680632-e146406c-3110-4713-848c-a2b8b332a5ed.png">
</p>

Анализируя графики, видим, что у 8cell процент метиллирования в CpG контексте составляет 42%, у icm 23%, у epiblast 77% - наибольший процент.
В то время как процент метиллирования в контексте CHG и CHH на каждой позиции у 8cell и icm составляет меньше процента, а для epiblast чуть больше процента.

 M-bias plots для Read2:
<p float="left">
 <img width="300" alt="Снимок экрана 2022-02-18 в 15 24 25" src="https://user-images.githubusercontent.com/91221560/154682611-fb21b1f4-e5b6-4ae3-b721-7df5468d4660.png">
 <img width="300" alt="Снимок экрана 2022-02-18 в 15 24 33" src="https://user-images.githubusercontent.com/91221560/154682623-a8b4211a-ccfc-42e2-92e6-8f702dca2673.png">
 <img width="300" alt="Снимок экрана 2022-02-18 в 15 24 46" src="https://user-images.githubusercontent.com/91221560/154682639-af198436-e08f-4998-a7a7-0e98567491b8.png">
</p>

Для Read2 у 8cell, icm и epibalst проценты метиллирования в CpG контексте на каждой позиции примерно 43%, 23% и 77% соответственно, но только у epiblast на позициях от 0 до 20 рост с 60% до ~77%. Что касается CHG и CHH контекста, в каждом образце на позициях начиная с 20 процент очень маленький, а от 0 до 20 процент снижается.

В мануале написано, что m-bias plot позволяет исследователям принять решение, оставлять ли bias в окончательных данных или же удалить его.

**Пункт (d)**

Получившиеся гистограммы для 8cell, icm и epiblast

(отображение насколько часто метилируются цитозины в данном образце: по X процент метилированных цитозинов, по Y - частота):

<img width="608" alt="Снимок экрана 2022-02-17 в 20 23 31" src="https://user-images.githubusercontent.com/91221560/154684758-b031b598-8a7e-4236-87ce-cc3fe9e373ba.png">
* Видно что наибольшая частота в 0%, от 20 до 60% метилированных цитозинов частота варьируется от 0 до 0.12, на 100% частота примерно 0.25

<img width="608" alt="Снимок экрана 2022-02-17 в 20 23 57" src="https://user-images.githubusercontent.com/91221560/154684799-04ce038f-7648-4d15-bcf8-15f207f69d04.png">
* Здесь тоже наибольшая частота в 0%, при остальных процентах частота уменьшилась по сравнению с 8cell

<img width="608" alt="Снимок экрана 2022-02-17 в 20 24 16" src="https://user-images.githubusercontent.com/91221560/154684808-afb6f932-14de-4bf5-bafa-89291a79ce60.png">
* Для epiblast видим противоположную картину: пик по частоте в 100% метилированных цитозинов

**Пункт (e)**
Визуализация уровня метилирования и покрытия для каждого образца:
<img width="1137" alt="Снимок экрана 2022-02-18 в 16 05 31" src="https://user-images.githubusercontent.com/91221560/154688235-b3577e43-7d58-43f7-a99d-0217c4f0b3b1.png">

<img width="1137" alt="Снимок экрана 2022-02-18 в 16 05 46" src="https://user-images.githubusercontent.com/91221560/154688255-23529f23-39fe-40a6-8e38-8442839db740.png">

