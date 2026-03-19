````
cat desired-state.txt
cat current-state.txt
��version: 1.0
app: myapp
replicas: 3
��version: 1.0
app: myapp
replicas: 3
````

````
./reconcile.sh
Thu Mar 19 13:35:29 MSK 2026 - ⚠️  DRIFT DETECTED!
Reconciling current state with desired state...
Thu Mar 19 13:35:29 MSK 2026 - ✅ Reconciliation complete
````

````
 diff desired-state.txt current-state.txt
cat current-state.txt
version: 1.0
app: myapp
replicas: 3
````

Цикл реконсиляции работает по принципу постоянного сравнения. Скрипт берет файл desired-state.txt (это источник истины из Git) и сравнивает его с current-state.txt (текущее состояние системы). Если содержимое файлов отличается, скрипт понимает, что произошел дрейф конфигурации (кто-то изменил настройки вручную). Чтобы исправить это, скрипт автоматически копирует желаемый файл поверх текущего. Это предотвращает дрейф, потому что система не ждет человека, а сама каждые 5 секунд проверяет соответствие и принудительно возвращает состояние к тому, что записано в репозитории.

## task 2

````
./healthcheck.sh
cat health.log
Thu Mar 19 13:41:08 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:41:08 MSK 2026 - ✅ OK: States synchronized
````
````
 ./healthcheck.sh
cat health.log
Thu Mar 19 13:44:27 MSK 2026 - ❌ CRITICAL: State mismatch detected!
  Desired MD5: a15a1a4f965ecd8f9e23a33a6b543155
  Current MD5: 48168ff3ab5ffc0214e81c7e2ee356f5
Thu Mar 19 13:41:08 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:44:27 MSK 2026 - ❌ CRITICAL: State mismatch detected!
  Desired MD5: a15a1a4f965ecd8f9e23a33a6b543155
  Current MD5: 48168ff3ab5ffc0214e81c7e2ee356f5
````

````
cat health.log
Thu Mar 19 13:44:44 MSK 2026 - ⚠️  DRIFT DETECTED!
Reconciling current state with desired state...
Thu Mar 19 13:44:44 MSK 2026 - ✅ Reconciliation complete
Thu Mar 19 13:44:44 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:41:08 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:44:27 MSK 2026 - ❌ CRITICAL: State mismatch detected!
  Desired MD5: a15a1a4f965ecd8f9e23a33a6b543155
  Current MD5: 48168ff3ab5ffc0214e81c7e2ee356f5
Thu Mar 19 13:44:44 MSK 2026 - ✅ OK: States synchronized
````
````
#!/bin/bash
# monitor.sh - Combined reconciliation and health monitoring
echo "Starting GitOps monitoring..."
echo "Starting GitOps monitoring..."
for i in {1..10}; dok #$i ---"
    echo "\n--- Check #$i ---"
    ./healthcheck.sh
    ./reconcile.sh
    sleep 3
done
Starting GitOps monitoring...
\n--- Check #1 ---
Thu Mar 19 13:45:47 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:45:47 MSK 2026 - ✅ States synchronized
\n--- Check #2 ---
Thu Mar 19 13:45:51 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:45:51 MSK 2026 - ✅ States synchronized
\n--- Check #3 ---
Thu Mar 19 13:45:54 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:45:54 MSK 2026 - ✅ States synchronized
\n--- Check #4 ---
Thu Mar 19 13:45:57 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:45:57 MSK 2026 - ✅ States synchronized
\n--- Check #5 ---
Thu Mar 19 13:46:00 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:00 MSK 2026 - ✅ States synchronized
\n--- Check #6 ---
Thu Mar 19 13:46:03 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:03 MSK 2026 - ✅ States synchronized
\n--- Check #7 ---
Thu Mar 19 13:46:05 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:05 MSK 2026 - ✅ States synchronized
\n--- Check #8 ---
Thu Mar 19 13:46:08 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:08 MSK 2026 - ✅ States synchronized
\n--- Check #9 ---
Thu Mar 19 13:46:11 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:11 MSK 2026 - ✅ States synchronized
\n--- Check #10 ---
Thu Mar 19 13:46:15 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:15 MSK 2026 - ✅ States synchronized
````

````
 cat health.log
Thu Mar 19 13:41:08 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:44:27 MSK 2026 - ❌ CRITICAL: State mismatch detected!
  Desired MD5: a15a1a4f965ecd8f9e23a33a6b543155
  Current MD5: 48168ff3ab5ffc0214e81c7e2ee356f5
Thu Mar 19 13:44:44 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:45:47 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:45:51 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:45:54 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:45:57 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:00 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:03 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:05 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:08 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:11 MSK 2026 - ✅ OK: States synchronized
Thu Mar 19 13:46:15 MSK 2026 - ✅ OK: States synchronized
````

Этот механизм работает так же, как статус синхронизации в ArgoCD. Когда хеши не совпадают, наш скрипт пишет "CRITICAL", а ArgoCD показывает статус "OutOfSync". Когда мы запускаем reconcile.sh для исправления — это аналог функции Auto-Sync в ArgoCD. Лог файл health.log выполняет ту же роль, что и панель мониторинга в GitOps-инструментах — хранит историю всех проверок и позволяет отследить, когда и насколько часто происходил дрейф конфигураци