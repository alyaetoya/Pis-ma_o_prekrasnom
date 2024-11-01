# Описание проекта
Проект, основаный на работе Д.Лихачёва "Письма о добром и прекрасном"
## Предобработка текста
Корпус включает одну крупную работу Дмитрия Сергеевича Лихачёва “Письма о добром и прекрасном”. Книга скачана из открытого доступа, для удобства работы текст был очищен от разделов оглавления, приветственной речи редактора, предисловия автора, сносок и сохранён в .txt-формате с сохранением авторской структуры. Несмотря на то, что корпус ограничен одной книгой, его несложно разбить на блоки по главам, чтобы затем использовать номера глав с названиями в качестве метаинформации. Это позволит пользователю быстро найти и ознакомиться с контекстом предложения из выдачи, если оно его заинтересовало. Главы книги имеют следующую структуру: “Письмо первое\n БОЛЬШОЕ В МАЛОМ\n Текст письма”. Номера писем и их названия были сохранены в переменную pattern, а содержимое в переменную content. Для связки метаинформации (pattern) с каждым блоком текста был использован метод списков словарей. Каждый словарь включает одно письмо и содержит:  
pattern: полное название письма (номер и название).  
content: список предложений (разбитый текст письма)  
После создания блоков с мета-информацией и текстом главы и проверкой их содержания, данные были занесены в csv-документ для удобства дальнейшей обработки (parsed_blocks.csv). Также была произведена небольшая корректировка неточностей.
## Морфологическая разметка корпуса
Выбор морфологического парсера для выполнения токенизации, лемматизации и POS-tagging пал на Stanza, так как именно он лучше всего проявил себя в ДЗ2 по параметру accuracy. Код принимал на вход parsed_blocks.csv и, проводя разметку в новых колонках, сохранял данные в parsed_blocks_with_nlp.csv. Из-за размера файла и долгой обработки было принято решение выдавать строки с предложениями порционно, по 100 штук. Таким образом, можно было отслеживать работу программы в реальном времени.
## Поиск словоформ и не только
Готовый код с поиском можно увидеть в файле SEARCH!.ipynb. Предполагается следующий формат запросов:  

search('поиск')  # Запрос на любую форму слова "поиск"  
search('"поиска"')  # Запрос на точную форму "поиска"    
search('NOUN VERB ADV')  # Запрос на последовательность POS-теггов  
search('ADJ дом')  # Запрос на прилагательное перед словом "дом"  
search('человек VERB "счастье" ,')  # Запрос на последовательность с разными критериями
