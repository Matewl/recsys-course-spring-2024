# Abstract
1 идея: DSSM дает на выходе не только список кандидатов, но и информацию о том, насколько эмбеддинги этих кандидатов близки эмбеддингу пользователя. Изначально они отсортированы в порядке увеличения расстояния до эмбеддинга пользователя. То есть лучше выдавать рекомендацию не случайно, а начиная с первого кандидата

2 идея: мы никак не используем фидбек от пользователя в рантайме. Предлагается получать фидбек и на основе него ранжировать кандидатов, которых дал  DSSM. Я использовал такое ранжирование: 
1) прослушанный трек всегда хуже непрослушанного. 
2) чем меньше пользователь прослушал трек, тем больше вес мы добавляем к треку, тем самым откидывая его дальше при сортировке.

# Детали 
Я добавил свою функцию ранжирования, которая выполняет функции, описанные в abstract. Эта функция называется MyIndexed и лежит в папке Indexed.py

В файле server.py есть глобальная переменная weighted_recs, в которой хранятся веса треков на протяжении всего эксперимента

# Результат
Получилось сильно улучшить обычный DSSM

![alt text](image.png)

# Инструкция
```commandline
cd ./botify
docker-compose up -d --build --force-recreate --scale recommender=1
cd ../sim
python -m sim.run --episodes 2000 --config config/env.yml multi --processes 4
cd ../botify
docker cp botify-recommender-1:/app/log/ /tmp/test
```
и запустить код первого семинара