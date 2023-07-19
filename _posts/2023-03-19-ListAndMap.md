---
title: "[java] List와 Map"
excerpt: "List와 Map"

categories:
  - java
tags:
  - [java]

permalink: /java/ListAndMap/

toc: false

date: 2023-03-19
last_modified_at: 2023-03-19
---

현대 분석철학의 바탕이 된 대표적 사상으로는 논리실증주의가 꼽힙니다. 논리실증주의 또는 논리경험주의는 과학적 논리적 분석 방법을 철학에 적용합니다. 논리실증주의는 검증 가능성을 중요하게 생각합니다. 명제를 검증할 수 있다면 의미가 있고, 검증할 수 없다면 의미가 없다고 여깁니다. 쉽게 말해 눈에 보이는 것은 의미가 있다고 여기지만 눈에 보이지 않는 것은 의미가 없다고 여깁니다. 그래서 논리실증주의에서 사랑이나 우정은 별로 중요하지 않습니다. 눈에 보이지 않으니까요.

백엔드와 프론트엔드의 차이점이 무엇이냐고 묻는다면 보이는 것과 보이지 않는 것의 차이라고 말하고 싶습니다. 프론트엔드는 눈에 보입니다. 백엔드는 눈에 보이지 않습니다. 메모리 어딘가에 데이터를 저장하고 반대로 출력하기도 합니다. 눈에 보이는 것도 중요하지만 때론 눈에 보이지 않는 것이 더 중요할 때도 있습니다. List나 Map에 값을 저장하는 것은 눈에 보이지 않는 것입니다. 이거 중요한 일입니다.

![ListAndMap](/assets/images/posts_img/ListAndMap.png)

## List에 값 저장&출력

사용자에게 입력값을 받아 List에 저장합니다. 저장된 값을 출력합니다.

```java
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.println("시작 값을 입력하세요");
        int startValue = input.nextInt();

        System.out.println("종료 값을 입력하세요");
        int endValue = input.nextInt();

        List<Integer> list = new ArrayList<>();

        if (startValue <= endValue) {
            while (startValue <= endValue) {
                list.add(startValue);
                startValue++;
            }
        } else {
            while (startValue >= endValue) {
                list.add(startValue);
                startValue--;
            }
        }

        System.out.println(list.toString());
        input.close();
    }
}

```

## Map에 값 저장&출력

```java
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Map<String, Object> map = new HashMap<>();

        System.out.println("Key-Value를 입력하세요.");
        System.out.println("종료하려면 exit 입력.");

        String input = "";
        while (!input.equals("exit")) {
            System.out.print("Key: ");
            String key = scanner.nextLine();

            System.out.print("Value: ");
            String value = scanner.nextLine();

            map.put(key, value);

            System.out.println("계속 입력하려면 아무 키나 입력하고, 종료하려면 exit를 입력하세요.");
            input = scanner.nextLine();
        }

        System.out.println("입력된 값:");
        for (String key : map.keySet()) {
            System.out.println(key + " = " + map.get(key));
        }
        scanner.close();
    }
}
```
