예제 5.1: 선형큐 프로그램
```
#include<stdio.h>						
#include<stdlib.h>
#define MAX_QUEUE_SIZE 5

typedef int element;
typedef struct {
	int front;
	int rear;
	element data[MAX_QUEUE_SIZE];
}QueueType;

void error(char* message) {						// 오류가 났을때 문자열을 받아 받은 문자열을 출력하는 프로그램
	fprintf(stderr, "%s\n", message);
	exit(1);
}

void init_queue(QueueType* q) {						// 큐를 -1로 초기화 하는 함수
	q->rear = -1;
	q->front = -1;
}

void queue_print(QueueType* q) {					// 큐를 출력하는수함수
	for (int i = 0; i < MAX_QUEUE_SIZE; i++) {
		if (i <= q->front || i > q->rear) {
			printf(" | ");
		}
		else {
			printf("%d | ", q->data[i]);
		}
		
	}
	printf("\n");
}

int is_full(QueueType* q) {						// 큐가 포화상태인지 검사하는 함수
	if (q->rear == MAX_QUEUE_SIZE - 1) {
		return 1;
	}
	else {
		return 0;
	}
}

int is_empty(QueueType* q) {						// 큐가 공백상태인지 검사하는 함수
	if (q->front == q->rear) {
		return 1;
	}
	else {
		return 0;
	}
}

void enqueue(QueueType* q, int item) {					// 큐에 삽입하는수함수
	if (is_full(q)) {
		error("큐가 포화상태입니다.");
		return;
	}
	q->data[++(q->rear)] = item;
}

int dequeue(QueueType* q) {						// 큐에서 삭제하는 함수
	if (is_empty(q)) {
		error("큐가 공백상태입니다.");
		return -1;
	}
	int item = q->data[++(q->front)];
	return item;
}

int main(void) {
	int item = 0;
	QueueType q;							//큐 객체를 지정한다

	init_queue(&q);

	enqueue(&q, 10); queue_print(&q);				
	enqueue(&q, 20); queue_print(&q);
	enqueue(&q, 30); queue_print(&q);
	
	item = dequeue(&q); queue_print(&q);
	item = dequeue(&q); queue_print(&q);
	item = dequeue(&q); queue_print(&q);
	return 0;
}
```
---
예제 5.2: 원형큐 프로그램
```
#include <stdio.h>
#include <stdlib.h>
#define MAX_QUEUE_SIZE 5

typedef int element;
typedef struct {
	element data[MAX_QUEUE_SIZE];
	int front, rear;
} QueueType;

void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

void init_queue(QueueType* q) {
	q->front = q->rear = 0;
}

int is_empty(QueueType* q) {
	return (q->front == q->rear);
}

int is_full(QueueType* q) {
	return ((q->rear + 1) % MAX_QUEUE_SIZE == q->front);
}

void queue_print(QueueType* q) {
	printf("QUEUE(front=%d rear=%d) = ", q->front, q->rear);
	if (!is_empty(q)) {
		int i = q->front;
		do {
			i = (i + 1) % (MAX_QUEUE_SIZE);
			printf("%d | ", q->data[i]);
			if (i == q->rear) {
				break;
			}
		} while (i != q->front);
	}
	printf("\n");
}

void enqueue(QueueType* q, element item) {
	if (is_full(q)) {
		error("큐가 포화상태입니다");
	}
	q->rear = (q->rear + 1) % MAX_QUEUE_SIZE;
	q->data[q->rear] = item;
}

element dequeue(QueueType* q) {
	if (is_empty(q)) {
		error("큐 공백상태입니다");
	}
	q->front = (q->front + 1) % MAX_QUEUE_SIZE;
	return q->data[q->front];
}

element peek(QueueType* q) {
	if (is_empty(q)) {
		error("큐가 공백상태입니다");
	}
	return q->data[(q->front + 1) % MAX_QUEUE_SIZE];
}

int main(void) {
	QueueType queue;
	int element;

	init_queue(&queue);

	printf("--데이터 추가 단계--\n");

	while (!is_full(&queue)) {
		printf("정수를 입력하시오: ");
		scanf("%d", &element);
		enqueue(&queue, element);
		queue_print(&queue);
	}
	printf("큐는 포화상태입니다. \n\n");

	printf("--데이터 삭제 단계--\n");
	while (!is_empty(&queue)) {
		element = dequeue(&queue);
		printf("꺼내진 정수: %d \n", element);
		queue_print(&queue);
	}
	printf("큐는 공백상태입니다.\n");
	return 0;
}
```
---
예제 5 - 3 큐 응용 프로그램
```
#include <stdio.h>
#include <stdlib.h>
#define MAX_QUEUE_SIZE 5

typedef int element;
typedef struct {
	element data[MAX_QUEUE_SIZE];
	int front, rear;
} QueueType;

void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

void init_queue(QueueType* q) {
	q->front = q->rear = 0;
}

int is_empty(QueueType* q) {
	return (q->front == q->rear);
}

int is_full(QueueType* q) {
	return ((q->rear + 1) % MAX_QUEUE_SIZE == q->front);
}

void queue_print(QueueType* q) {
	printf("QUEUE(front=%d rear=%d) = ", q->front, q->rear);
	if (!is_empty(q)) {
		int i = q->front;
		do {
			i = (i + 1) % (MAX_QUEUE_SIZE);
			printf("%d | ", q->data[i]);
			if (i == q->rear) {
				break;
			}
		} while (i != q->front);
	}
	printf("\n");
}

void enqueue(QueueType* q, element item) {
	if (is_full(q)) {
		error("큐가 포화상태입니다");
	}
	q->rear = (q->rear + 1) % MAX_QUEUE_SIZE;
	q->data[q->rear] = item;
}

element dequeue(QueueType* q) {
	if (is_empty(q)) {
		error("큐 공백상태입니다");
	}
	q->front = (q->front + 1) % MAX_QUEUE_SIZE;
	return q->data[q->front];
}

element peek(QueueType* q) {
	if (is_empty(q)) {
		error("큐가 공백상태입니다");
	}
	return q->data[(q->front + 1) % MAX_QUEUE_SIZE];
}

int main() {
	QueueType queue;
	int element;

	init_queue(&queue);

	printf("--데이터 추가 단계--\n");
	while (!is_full(&queue)) {
		printf("정수를 입력하시오: ");
		scanf("%d", &element);
		enqueue(&queue, element);
		queue_print(&queue);
	}
	printf("큐는 포화상태입니다.\n\n");

	printf("--데이터 삭제 단계--\n");

	while (!is_empty(&queue)) {
		element = dequeue(&queue);
		printf("꺼내어진 정수: %d \n", element);
		queue_print(&queue);
	}
	printf("큐는 공백상태입니다. \n");
}
```
---
예제 5 - 4 원형 덱 프로그램
```
#include <stdio.h>
#include <stdlib.h>
#define MAX_QUEUE_SIZE 5

typedef int element;
typedef struct {
	element data[MAX_QUEUE_SIZE];
	int front, rear;
} DequeType;

void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

void init_deque(DequeType* q) {
	q->front = q->rear = 0;
}

int is_empty(DequeType* q) {
	return (q->front == q->rear);
}

int is_full(DequeType* q) {
	return ((q->rear + 1) % MAX_QUEUE_SIZE == q->front);
}

void depue_print(DequeType* q) {
	printf("Deque(front=%d rear=%d) = ", q->front, q->rear);
	if (!is_empty(q)) {
		int i = q->front;
		do {
			i = (i + 1) % (MAX_QUEUE_SIZE);
			printf("%d | ", q->data[i]);
			if (i == q->rear) {
				break;
			}
		} while (i != q->front);
	}
	printf("\n");
}

void add_rear(DequeType* q, element item) {
	if (is_full(q)) {
		error("큐가 포화상태입니다.");
	}
	q->rear = (q->rear + 1) % MAX_QUEUE_SIZE;
	q->data[q->rear] = item;
}

element delete_front(DequeType* q) {
	if (is_empty(q)) {
		error("큐가 공백상태입니다.");
	}
	q->front = (q->front + 1) % MAX_QUEUE_SIZE;
	return q->data[q->front];
}

void add_front(DequeType* q, element val) {
	if (is_full(q)) {
		error("큐가 포화상태입니다.");
	}
	q->data[q->front] = val;
	q->front = (q->front - 1 + MAX_QUEUE_SIZE) % MAX_QUEUE_SIZE;
}

element delete_rear(DequeType* q) {
	int prev = q->rear;
	if (is_empty(q)) {
		error("큐가 공백상태입니다.");
	}
	q->rear = (q->rear - 1 + MAX_QUEUE_SIZE) % MAX_QUEUE_SIZE;
	return q->data[prev];
}

element get_rear(DequeType* q) {
	if (is_empty(q)) {
		error("큐가 공백상태입니다");
	}
	return q->data[q->rear];
}

int main() {
	DequeType queue;

	init_deque(&queue);

	for (int i = 0; i < 3; i++) {
		add_front(&queue, i);
		depue_print(&queue);
	}
	for (int i = 0; i < 3; i++) {
		delete_rear(&queue);
		depue_print(&queue);
	}
	return 0;
}
```