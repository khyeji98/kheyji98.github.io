---
comments: true
title: Swift ) 순환 버퍼(Ring Buffer)
key: 202103091
modify_date: 2021-03-09
picture_frame: shadow
tags:
  - [Algorithm]
  - [데이터 구조]
---
 
## 순환 버퍼(Ring Buffer)
 
순환 버퍼는 **고정 크기의 데이터 구조**로, Ring의 구조와 비슷하다.   
만약 버퍼가 데이터로 꽉 차면 버퍼의 시작 부분을 뜻하는 헤드 인덱스가 0으로 되돌아 가며, 기존 데이터 중 가장 먼저 저장된 데이터가 밀려나고 새로운 데이터가 저장된다.   
 
이러한 특징으로 인해 순환 버퍼는 특히 **FIFO** 데이터 구조를 구현할 때 유용하다.   
큐 데이터 구조 역시 FIFO와 같은 형식이지만 순환 버퍼는 **헤드 인덱스와 테일 인덱스가 맞물려 있다는 점**에서 다르다.
 
```
public struct RingBuffer<T> { 
    private var array: [T?]
    private var readIndex = 0 
    private var writeIndex = 0 
    
    public init(count: Int) {
        array = Array<T?>(repeating: nil, count: count)
    }
    
    public var first: T? {
        // readIndex가 큐의 첫번째 값
        array[readIndex]
    } 
    
    public mutating func write(_ element: T) -> Bool { 
        if !isFull {
            array[writeIndex % array.count] = element 
            writeIndex += 1
            return true
        } else {
            return false 
        }
    }
    
    public mutating func read() -> T? { 
        if !isEmpty {
            let element = array[readIndex % array.count]
            readIndex += 1 
            return element 
        } else {
            return nil 
        }
    }
    
    private var availableSpaceForReading: Int {
        writeIndex - readIndex 
    }
    
    public var isEmpty: Bool {
        availableSpaceForReading == 0
    }
    
    private var availableSpaceForWriting: Int {
        array.count - availableSpaceForReading 
    }
    
    public var isFull: Bool {
        availableSpaceForWriting == 0
    }
}
```
여기까지는 떠뜸떠뜸 이해했는데, 이 다음부터 다시 이해 안되기 시작..
```
extension RingBuffer: CustomStringConvertible { 
    public var description: String {
        let values = (0..<availableSpaceForReading).map {
            String(describing: array[($0 + readIndex) % array.count]!)
        }
        return "[" + values.joined(separator: ", ") + "]"
    }
}
```
알고보니 `CustomStringConvertible`은 결과 디버깅과 테스트를 용이하게 하기 위해 준수하는 프로토콜이라고 한다..ㅎ   
뜯어보면 `availableSpaceForReading`은 읽을 수 있는 요소 카운트이므로 "아직 제거되지 않은 값부터 새로 추가된 값까지"를 나타내는 것이다.   
그리고 그 범위만큼 map함수를 돌린다는 것이다.   
그렇다면 **순환 버퍼**이기 때문에 어차피 0..<5 일 것이다.
 

 
그리고 이제 **제네릭 구조체**인 QueueRingBuffer를 정의해보자.
```
public struct QueueRingBuffer<T>: Queue { 
    private var ringBuffer: RingBuffer<T> 
    
    public init(count: Int) {
        ringBuffer = RingBuffer<T>(count: count)
    }
    
    public var isEmpty: Bool {
        ringBuffer.isEmpty 
    }
    
    public var peek: T? {
        ringBuffer.first 
    }
    
    // 큐에 요소 추가
    public mutating func enqueue(_ element: T) -> Bool { 
        // 요소 추가에 성공하면 true, 실패하면 false 반환(고정된 크기라서 실패할 수도 있음)
        ringBuffer.write(element) 
    }
    
    // 큐의 앞에서 요소 삭제
    public mutating func dequeue() -> T? {
        // ringBuffer가 비어있는지 체크하고, 만약 비어있다면 nil 반환
        ringBuffer.read()
    }
}
```
순환 버퍼는 크기가 고정된 버퍼이기 때문에 반드시! **count** 파라미터를 포함해야 한다.   
 
그리고 `Queue` 프로토콜을 상속하기 때문에 `isEmpty`와 `peek` 프로퍼티를 생성했으며, 이 변수들은 ringBuffer를 노출시키지 않고 큐의 앞 요소에 접근하여 큐가 비어있는지 확인한다.
```
extension QueueRingBuffer: CustomStringConvertible {
    public var description: String {
        String(describing: ringBuffer)
    }
}
```
QueueRingBuffer 역시 결과 디버깅과 테스트를 용이하게 하기 위해 CustomStringConvertible 프로토콜을 준수한다.   
이 코드는 큐 내부의 ringBuffer에 위임하여 큐의 문자열 표현을 생성한다.
 
```
var queue = QueueRingBuffer<String>(count: 10) 
queue.enqueue("Kim")
queue.enqueue("Jung")
queue.enqueue("Yoon")
queue 
queue.dequeue()
queue
queue.peek
```
 
### 장점
 
- 배열 데이터 구조보다 데이터 저장에 효율적이다.
- 버퍼의 메모리 크기가 안정적인 상태를 유지한다.
- 구현할 때, 버퍼의 크기를 조절하고 기존의 데이터를 새로 생성된 버퍼로 전달하는 기능이 추가된다.
 
#### Reference)
 
[https://iospanda.tistory.com/entry/Swift-Queue-Ring-Buffer-Double-Stack%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-Queue-%EA%B5%AC%ED%98%84%EA%B3%BC-%EA%B7%B8-%EC%98%88](https://iospanda.tistory.com/entry/Swift-Queue-Ring-Buffer-Double-Stack%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-Queue-%EA%B5%AC%ED%98%84%EA%B3%BC-%EA%B7%B8-%EC%98%88)   
[https://the-brain-of-sic2.tistory.com/22](https://the-brain-of-sic2.tistory.com/22)
