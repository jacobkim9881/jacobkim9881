포스트:

https://velog.io/write?id=b4ebff22-4f97-4422-8a56-d49d7c472c0a

## 코파일럿의 등장
최근 AI 기술의 발전으로 정보를 얻는 방식이 획기적으로 변했다.  
특히 코파일럿의 등장 덕분에 **광범위한 정보 검색과 정리**가 간편해졌다.  
덕분에 우리는 **더 많은 정보를 빠르게 확보**할 수 있으며, 이를 효과적으로 활용하는 방법도 고민할 수 있다.  

![](https://velog.velcdn.com/images/jacobkim9881/post/e57f5f72-d50e-4986-ba8a-0a9ece2a2b07/image.png)

코파일럿은 **Markdown 포맷**으로 정보를 제공할 수 있어 `.md` 파일로 저장하기에 최적화되어 있다.  
하지만 이렇게 `.md` 파일이 늘어나면 **주제별로 파일을 관리하기가 어려워질 수 있다.**  

![](https://velog.velcdn.com/images/jacobkim9881/post/ba4a3798-702f-4734-a340-e8c2fe08b59b/image.png)


## 코파일럿의 활용

![](https://velog.velcdn.com/images/jacobkim9881/post/b8ad77ba-0697-4554-b5ab-064bc9a7089c/image.png)


이 문제를 해결하기 위해 **자동화된 파일 정리 시스템**을 만들기로 했다.  
각 `.md` 파일 내부의 **헤더(`#`)를 추출하여 하나의 파일(`HEADERS.md`)로 정리**하면  
주제별 흐름을 쉽게 파악할 수 있기 때문이다.  

이를 위해 **자동 실행 파일을 만들고, 코파일럿의 도움을 받아 간단한 스크립트를 제작**했다.  
내 역할은 방향을 설정하고 지시를 내리는 것이었고, 코파일럿이 코드를 작성해주었다.  

## 코파일럿으로 얻은 정보로 통찰력 얻기
이렇게 생성된 `HEADERS.md` 파일을 활용하면  
어떤 주제의 흐름을 한눈에 파악할 수 있어 **정보 탐색이 훨씬 효율적으로 이루어진다.**  

예를 들어, 여러 `.md` 파일이 저장된 폴더에서  
**각 파일의 주요 제목과 소제목을 빠르게 확인하고 전체적인 개요를 정리**할 수 있다.  

## `.md` 파일에서 헤더 추출하기
이를 자동화하기 위해 `"eh-auto-win.bat"`이라는 **실행 파일**을 만들었다.  
이 파일을 더블 클릭하면 `.md` 파일 내부의 헤더(`#`)를 추출하여 `HEADERS.md`로 정리한다.  

### 🔹 `eh-auto-win.bat` 파일 구조
```batch
@echo off
bash eh-auto.sh
pause
```

✅ 이 실행 파일은 같은 폴더 안의 `"eh-auto.sh"` **쉘 스크립트**를 실행한다.  

하지만 나는 **배치 스크립트에 대한 지식이 거의 없었다.**  
코파일럿의 도움을 받아 단순 실행만 가능하도록 설정했다.  

### 🔹 `eh-auto.sh` 쉘 스크립트
```bash
#!/bin/bash

OUTPUT_FILE="HEADERS.md"

# ✅ 기존 파일 삭제
rm -f "$OUTPUT_FILE"

# ✅ 폴더와 파일을 처리하는 재귀 함수
process_directory() {
    local DIR=$1
    local FILES=$(ls -p "$DIR" | grep -v /)  # ✅ 현재 폴더의 파일 (.md 파일만 포함)
    local FOLDERS=$(ls -p "$DIR" | grep /)   # ✅ 현재 폴더의 서브 폴더 (폴더명 포함)

    # ✅ 현재 폴더의 `.md` 파일 처리
    for file in $FILES; do
        if [[ $file == *.md ]]; then
            echo "$DIR/$file" >> "$OUTPUT_FILE"  # ✅ 파일 경로 추가
            grep '^#' "$DIR/$file" >> "$OUTPUT_FILE"  # ✅ `#` 포함된 문장 추출
            echo -e "\n\n" >> "$OUTPUT_FILE"  # ✅ 마지막 줄 다음 2줄 띄우기
        fi
    done

    # ✅ 폴더 내부 `.md` 파일 검색 (재귀 호출)
    for folder in $FOLDERS; do
        process_directory "$DIR/$folder"
    done
}

# ✅ 초기 디렉토리에서 실행 (현재 폴더)
process_directory "."

echo "🎉 모든 폴더의 .md 파일을 HEADERS.md에 정리 완료!"
```

✅ 이 쉘 스크립트는 **현재 폴더 및 모든 서브 폴더의 `.md` 파일**을 탐색하여  
각 파일의 헤더(`#`)를 추출하고 **`HEADERS.md`에 정리**하는 역할을 한다.  

## 코파일럿과 자동화의 미래
나는 **코드 한 줄도 작성하지 않았지만**, 이 시스템을 완성할 수 있었다.  
마치 **건설 현장에서 나는 감독이고, 코파일럿이 작업을 수행하는 인부처럼** 느껴졌다.  

이제는 **코드 작성이 더 이상 개발자의 전유물이 아니며**,  
아이디어만 있다면 누구나 코딩을 활용해 원하는 자동화를 구현할 수 있는 시대가 온 것이다.  

✅ **자동화된 `.md` 파일 정리 시스템**은 정보 관리의 효율성을 극대화한다.  
✅ **코파일럿을 활용하면 최소한의 노력으로 강력한 기능을 구현 가능하다.**  
✅ **앞으로 AI 기술과 자동화가 더 발전하면 더 창의적인 활용이 가능할 것이다.**  

🔥 **앞으로도 코파일럿과 함께 더 많은 자동화 시스템을 만들어가고 싶다!** 🚀


# Copilot and Automation: Organizing `.md` File Headers

## The Rise of Copilot
The rapid advancement of AI technology has revolutionized the way we acquire information.  
With the emergence of Copilot, **searching for and organizing vast amounts of information has become much easier.**  
Thanks to this, we can **quickly gather extensive data** and consider how to use it more effectively.  

Copilot provides information in **Markdown format**, making it convenient to store in `.md` files.  
However, as the number of `.md` files grows, **managing them by topic can become challenging.**  

## Utilizing Copilot
To solve this problem, I decided to **create an automated file organization system**.  
By extracting **headers (`#`) from `.md` files and consolidating them into a single `HEADERS.md` file**,  
I could easily grasp the overall structure of various topics.  

For this, I created **an executable file** with the help of Copilot, which provided simple script automation.  
My role was to set the direction and issue commands, while Copilot wrote the code for me.  

## Gaining Insights from Copilot-Acquired Information
With the `HEADERS.md` file,  
I can now understand a topic’s overall flow at a glance, making **information exploration much more efficient.**  

For example, within a folder containing multiple `.md` files,  
I can **quickly review their major headings and subheadings, making it easier to organize comprehensive insights.**  

## Extracting Headers from `.md` Files
To automate this process, I created an **executable file** called `"eh-auto-win.bat"`.  
By double-clicking this file, it extracts headers (`#`) from `.md` files and consolidates them into `HEADERS.md`.  

### 🔹 Structure of `eh-auto-win.bat`
```batch
@echo off
bash eh-auto.sh
pause
```

✅ This executable runs the `"eh-auto.sh"` **shell script** located in the same folder.  

I had **no prior knowledge of batch scripting**,  
but thanks to Copilot’s assistance, I was able to set up a simple execution file without errors.  

### 🔹 `eh-auto.sh` Shell Script
```bash
#!/bin/bash

OUTPUT_FILE="HEADERS.md"

# ✅ Remove existing file
rm -f "$OUTPUT_FILE"

# ✅ Recursive function to process folders and files
process_directory() {
    local DIR=$1
    local FILES=$(ls -p "$DIR" | grep -v /)  # ✅ List non-folder `.md` files in the current directory
    local FOLDERS=$(ls -p "$DIR" | grep /)   # ✅ Identify subdirectories

    # ✅ Extract headers from `.md` files
    for file in $FILES; do
        if [[ $file == *.md ]]; then
            echo "$DIR/$file" >> "$OUTPUT_FILE"  # ✅ Add file path to output
            grep '^#' "$DIR/$file" >> "$OUTPUT_FILE"  # ✅ Extract lines containing `#` and append them
            echo -e "\n\n" >> "$OUTPUT_FILE"  # ✅ Add spacing for readability
        fi
    done

    # ✅ Recursively process subdirectories
    for folder in $FOLDERS; do
        process_directory "$DIR/$folder"
    done
}

# ✅ Start processing from the current directory
process_directory "."

echo "🎉 Successfully compiled all `.md` headers into HEADERS.md!"
```

✅ This shell script **searches all `.md` files—including those in subdirectories—recursively**,  
extracts all headers (`#`), and **compiles them into `HEADERS.md`.**  

## The Future of Copilot and Automation
Without writing a single line of code myself, I was able to **complete this automation system.**  
It felt like **I was the director on a film set, while Copilot played the role of the lead actor.**  

Now, **coding is no longer exclusive to developers.**  
With the right ideas, **anyone can leverage AI-powered automation to achieve their goals effortlessly.**  

✅ **This automated `.md` file organization system greatly improves information management efficiency.**  
✅ **Using Copilot minimizes effort while still delivering powerful functionality.**  
✅ **As AI technology continues to evolve, we can expect even more creative applications in the future.**  

🔥 **I look forward to creating more automation systems with Copilot!** 🚀
```