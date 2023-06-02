# DnD 5e LaTeX Template - 한국어판

[DnD 5e LaTeX Template](https://github.com/rpgtex/DND-5e-LaTeX-Template)의 한국어 포크입니다.
DKSA의 [D&D 5판 번역](https://www.dndkr.com/support)과 일관성을 맞추려 노력했습니다. 

## 기능

* 컬러 스킴, 폰트 및 레이아웃이 코어 룰북과 유사합니다. (완전히 같지는 않습니다.)
* 폰트가 기본적으로 내장돼 있습니다.
* LuaTeX 및 XeTeX에서 사용할 수 있습니다.

<img src="preview-ko.png" alt="preview" width="637">

## 왜 원본과 따로 배포하나요?

여기서 작업한 것을 원본 프로젝트에 풀 리퀘스트를 통해 반영하는 것이 이상적이긴 합니다.\\*
그러나 LaTeX에서 한글 폰트 입력 시 발생하는 여러 이슈 및 한국어 특유의 서식으로 인해 프로젝트를 분리했습니다.

### 원본 프로젝트와의 차이점

기본적으로 원본 프로젝트 파일을 그대로 유지하고 한국어 지원을 위한 설정을 새 파일로 오버라이드하는 방식입니다.\\*
따라서 원본 프로젝트의 기능을 동일하게 사용할 수 있으며 한국어를 위한 몇가지 추가 기능을 지원합니다.\\*
한국어 폰트 사용을 위해 fontspec 패키지를 사용하므로 pdfLaTeX 대신 LuaLaTeX, XeLaTeX 등의 컴파일러를 사용해야 합니다.

## 설치

크게 두 가지 설치 방식이 있습니다.\\*
별도 설치 없이 저장소를 클론한 후 해당 디렉토리 내에서 바로 LaTeX 명령어를 사용해 예제 파일을 빌드할 수도 있습니다.

### `TEXMFHOME`을 이용한 사용자 설치 (권장)

이 방식은 현재 시스템 사용자의 다음 경로에 템플릿을 설치합니다.

* Linux: `~/.texmf/tex/latex`
* OS X / macOS: `~/Library/texmf/tex/latex`
* Windows: `C:\Users\{username}\texmf\tex\latex`

이렇게 설치된 템플릿은 LaTeX에 의해 자동으로 감지되어 사용할 수 있습니다.

1. `TEXMFHOME` 디렉토리가 없을 경우 새로 생성합니다.

    ```sh
    mkdir "$(kpsewhich -var-value TEXMFHOME)"
    ```

2. [최신 버전](https://github.com/ShoyuVanilla/DND-5e-LaTeX-Template-Korean/releases/latest)을 다운받아 `$TEXMFHOME`에 압축을 해제합니다.

    ```sh
    cd "$(kpsewhich -var-value TEXMFHOME)"
    curl -o dndko.tds.zip https://github.com/ShoyuVanilla/DND-5e-LaTeX-Template-Korean/releases/latest
    bsdtar --strip-components=1 -xvf dndko.tds.zip
    rm dndko.tds.zip
    ```

### Overleaf

[Overleaf](https://overleaf.com)는 구글 독스와 비슷한 방식의 온라인 TeX 편집기입니다.\\*
이 방식은 로컬에 TeX를 직접 설치할 필요가 없으며 일회성 프로젝트에 이상적입니다.

다음 [링크](https://www.overleaf.com/latex/templates/d-and-d-5e-latex-korean-template/dczdnwwcxbzt)에서 템플릿을 불러올 수도 있고 아래
방법을 통해 직접 프로젝트를 생성할 수도 있습니다.

1. 윗쪽의 *Clone or download* 버튼을 클릭해 이 GitHub 저장소를 ZIP 파일로 다운받습니다.
2. Overleaf에서 *New Project* 버튼을 클릭한 후 *Upload Project*를 선택합니다 이 저장소에서 다운받은 ZIP .

## 사용법

### 클래스 (권장)

문서 서두에서 `dndbook-ko` 클래스를 호출합니다.

```tex
\documentclass[10pt,twoside,twocolumn,openany,nodeprecatedcode]{dndbook-ko}

\begin{document}
% ...
```

### 패키지

`dnd-ko` 패키지를 직접 호출해 다른 클래스와 함께 사용할 수도 있습니다.
테스트한 패키지는 `book` 클래스 뿐입니다.

```tex
\documentclass[10pt,twoside,twocolumn,openany]{book}

\usepackage[layout=true]{dnd-ko}

\begin{document}
% ...
```

### 옵션

| Option         | Package `dnd-ko`| Class `dndbook-ko`|
| -------------- | :-------------: | :---------------: |
| `bg`           | ✓               | ✓                 |
| `justified`    | ✓               | ✓                 |
| `layout`       | ✓               |                   |
| `nomultitoc`   | ✓               | ✓                 |
| `nodeprecatedcode`   | ✓               | ✓                 |

`dndbook-ko` 클래스는`book` 클래스의 모든 옵션을 지원합니다.

#### `bg`

배경 및 꼬리말 이미지를 불러오는 방식을 선언합니다. 다음과 같은 value를 통해 key-value 옵션으로 설정할 수 있습니다.

* `full`: 배경과 꼬리말 이미지를 모두 불러옵니다. (**기본값**)
* `none`: 배경과 꼬리말 이미지를 모두 제거합니다.
* `print`: 꼬리말 이미지만 불러옵니다.

#### `justified`

본문의 행의 끝을 나란히 맞춥니다.

#### `layout`

`dnd-ko` 패키지가 문서 레이아웃도 변경할 것인지를 결정합니다. (geometry, colors, typography 등)
다음과 같은 값을 지정할 수 있는 불리언 옵션입니다.

* `true`: 문서 레이아웃을 변경합니다.
* `false`: 문서 레이아웃을 변경하지 않습니다.

초기 버전과의 하위 호환성을 위해 기본값은 `true` 입니다.
향후 배포 버전에서는 변경될 것입니다.

#### `nomultitoc`

목차를 여러 단으로 표시하지 않습니다.

#### `nodeprecatedcode`

deprecated된 코드를 빌드 과정에서 제외합니다.

## Dependencies

LaTeX을 설치하지 않았다면 [TeX Live 배포판](https://www.tug.org/texlive/)을 설치하실 것을 권장합니다.

### Ubuntu

```sh
sudo apt-get install texlive-full
```

### Arch

```sh
sudo pacman -S texlive-bin texlive-core texlive-latexextra
```

### OS X

MacTex [인스톨러](https://www.tug.org/mactex/)를 통해 설치할 수도 있지만 brew cask 명령어를 통해서도 설치할 수 있습니다.

#### 풀 버전

```sh
brew cask install mactex
```

#### GUI가 없는 좀 더 가벼운 버전

```sh
brew cask install mactex-no-gui
```

#### 미니멀 버전

`tlmgr` 명령어를 통해 필요한 패키지만 설치합니다. 좀 더 자세한 사항은 다음 [답변](https://tex.stackexchange.com/a/470285)을 참고해 주십시오.

```sh
brew cask install basictex
brew cask install tex-live-utility
```

위 버전 중 어느 것으로든 설치가 끝나면 다음 명령어를 이용해 texlive 디렉토리에 관리자 권한이 필요하지 않도록 설정합니다.

```sh
sudo chown -R myuser:mygroup /usr/local/texlive
```

MacTex 권한 문제에 대해서는 StackExchange [게시물](https://tex.stackexchange.com/questions/3744/how-do-i-set-up-mactex-so-admin-rights-arent-necessary)을 참고하십시오.

## 알려진 이슈 및 해결책

### 스탯 블록이 페이지를 넘어가면 텍스트 색상이 유지되지 않습니다

`tcolorbox` 패키지와 관련된 이슈입니다. `tcolorbox` 매뉴얼의 4.12 절에도 다음과 같이 나와 있습니다. (363 )

> If your text content contains some text color changing commands, your color will not survive the break to the next box.

이 경우 문서 컴파일에 LuaTeX을 사용하십시오.

```sh
lualatex main.tex
```

### `monsterbox`를 float으로 감싸면 스탯 블록 내부의 여백이 망가집니다

다음과 같이 `monsterbox` 또는 `monsterboxnobg`를 floating figure 안에 넣으면 스탯 블록 구성요소 사이에 여백이 더 생깁니다.

```latex
\begin{figure}[b]
  \begin{monsterbox}{Orc Warden}
    % ...
  \end{monsterbox}
\end{figure}
```

이 경우 `tcolorbox` 의 `float` 패러미터를 사용하십시오.

```latex
\begin{monsterbox}[float=b]{Orc Warden}
  % ...
\end{monsterbox}
```

`float` 패러미터와 관련된 자세한 사항은 `tcolorbox` 공식 문서의 4.13 절을 참고하십시오.

### 폰트가 D&D 공식 한국어판과 조금 다릅니다

본문을 비롯한 대부분의 폰트는 D&D 공식 한국어판에서 사용한 폰트를 그대로 사용했으나 Mrs Eaves Small Caps(장, 절 영문 제목)를 비롯한 몇몇 폰트는 라이선스 문제로 사용하지 못했습니다.
해당 폰트들을 대신해 사용할 수 있는 몇 가지 대체 폰트는 [이곳](https://github.com/jonathonf/solbera-dnd-fonts)에서 구할 수 있습니다.
이 폰트 역시 라이선스 문제로 본 프로젝트에 포함시키지는 못했습니다.

## 향후 계획

* 지속적인 원본 프로젝트 변경사항 
* 표지 폰트 및 양식 지원
* 부록(Appendix) 양식 지원
* 장, 절 제목 영문 폰트를 별도 명령 없이 자동 지정

## Credits

* [Original project](https://github.com/rpgtex/DND-5e-LaTeX-Template) by [rpgtex](https://github.com/rpgtex) team
* Background image from [Lost and Taken](https://lostandtaken.com/)

## License

MIT License

### Fonts

* IMFellGreatPrimer(장, 절 영문 제목), Noto Sans KR(스탯 블록), Noto Serif KR(장, 절 제목), 나눔명조(큰 첫머리 글자) - SIL Open Font License
* 함초롬바탕(본문) - 한글과컴퓨터
