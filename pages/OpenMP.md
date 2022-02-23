- 공유 메모리 다중 처리 프로그래밍 API로, C, C++, 포트란 언어와, 유닉스 및 마이크로소프트 윈도우 플랫폼을 비롯한 여러 플랫폼을 지원한다.
- # Todo
- ```
  #include <stdlib.h>
  #include <stdio.h>
  #include <math.h>
  #include <omp.h>
  
  // 10 million
  #define N 10000000
  
  int main() {
    // step size
    double h = 1 ./ (N + 1);
  
    // start timer
    double t = omp_get_wtime();
    double quarterpi = 0.;
    #pragma omp parallel for reduction(+:quarterpi)
    for (int i = 0; i < N; i++) {
      double x = i * h;
      quarterpi += h * sqrt(1 - x * x);
    }
    // stop timer and report
    t = omp_get_wtime() - t;
    #pragma omp parallel
  
    if (omp_get_thread_num() == 0) {
      printf(
        "Pi=%8.4f in time on %2d threads: %7.5f\n", 
        4 * quarterpi,
        omp_get_num_threads(),
        t
      );
    }
    return 0;
  }
  
  ```
- https://qr.ae/pGQCFB
- # Reference
- https://ko.wikipedia.org/wiki/OpenMP