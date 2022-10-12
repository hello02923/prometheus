## Docker-Prometheus

搭配著看的
- [[Day27] 簡單搞懂 Prometheus 是什麼？](https://ithelp.ithome.com.tw/articles/10307286)
- [[Day28] 簡單搞懂Prometheus Docker實作範例](https://ithelp.ithome.com.tw/articles/10307312)
- [[Day29] 簡單搞懂Promethues Python FastAPI 實作範例]()
```
docker-prometheus/
├── alertmanager
│   └── config.yml
├── docker-compose.yml
├── grafana
│   ├── config.monitoring
│   └── provisioning
└── prometheus
    ├── alert.yml
    └── prometheus.yml
```

- 參考文件
1. https://yunlzheng.gitbook.io/prometheus-book/parti-prometheus-ji-chu/promql/prometheus-metrics-types
2. https://www.twblogs.net/a/605872dab586f7f7095f4fe7(python 應用在prometheus)
3. https://blog.csdn.net/shm19990131/article/details/107162470
4. https://linuxhint.com/monitor-python-applications-prometheus/
5. https://github.com/prometheus/client_python 
6. https://awesome-prometheus-alerts.grep.to/rules.html (常見alert 規則)
7. https://www.cnblogs.com/robinunix/p/11276296.html (node-exporter 指標含義)
8. https://blog.csdn.net/shm19990131/article/details/107162470 (node-exporter cpu 基礎)
9. https://pracucci.com/prometheus-understanding-the-delays-on-alerting.html(解釋警報延遲文章)
10. https://blog.techbridge.cc/2019/08/26/how-to-use-prometheus-grafana-in-flask-app/
11. https://github.com/Kev1nChan/docker-prometheus

# 常見四大功能
- Counter 計數器 只增不減（除非系统发生重置）
    - 常見指標：prometheus_http_requests_total，cpu狀況（還未測試）
        ex. topk(10,prometheus_http_requests_total) : 訪問量前10的http address
        ex. rate(rate(request_count_total[10m])): 看10分鐘的request 總數增長率
- Gauge 可增可減 指標側重於反應系統的當前狀態 
    ex. node_cpu_seconds_total: cpu使用量 
        => delta(node_cpu_seconds_total[5m]) : cpu 在五分鐘的使用量 delta是取一段時間 
        => delta(node_cpu_seconds_total{mode='idle'}[2h]): 空閒的cpu 在兩小時的使用量
    ex. deriv()計算樣本的線性回歸模型

- Histogram
- Summary


# 測試情境
- 寄信條件
1. server 掛了
2. request 超過一定量
3. exceptions 超過一定量

# 測試工具
- 文件
1. https://www.twblogs.net/a/5c76c100bd9eee33991815b9
2. https://blog.csdn.net/wumingxiaoyao/article/details/120799713
3. https://docs.locust.io/en/stable/writing-a-locustfile.html#taskset-class
4. https://danielflannery.ie/simulate-cpu-load-with-python/ (模擬cpu loading by python)
5. https://blog.techbridge.cc/2019/05/29/how-to-use-python-locust-to-do-load-testing/ (教學文章)
6. https://www.tigera.io/learn/guides/prometheus-monitoring/prometheus-metrics/


指令locust -f test.py
打開http://localhost:8089/ 做測試
