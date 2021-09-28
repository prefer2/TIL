## NPM

Node Package Manager의 줄임말. Node.js의 패키지들을 관리할 수 있는 도구.

`npm init`: create a package.json file which is kind of a configuration file of a project.

`npm install 패키지이름`: 패키지 install

`npm install 패키지이름  —save-dev`: dependency. webpack, debug tool, testing library 등 개발 단계에 필요한 의존성 파일들을 install

`npm install 패키지이름 —global`: 시스템 폴더에 패키지를 설치. 주로 development dependencies를 global하게 설치함. -g 플래그를 사용할 경우 package.json 의 의존성 목록에 기록되지 않는다.

install은 i로, global은 g로 줄여 쓸 수 있다.


### npm script

`npm run 스크립트`  원하는 명령어를 간단하게 사용할 수 있음.

### version

`major version. minor version. patch version`

patch version: fix bugs

minor version: includes new feature but it does not include breaking changes. minor version은 바뀌어도 기존에 사용하던 코드를 사용하는데는 문제 없다.

major version: huge new release which can have breaking changes.

`npm outdated` : update가 필요한 package들을 table로 보여준다.

`npm update 패키지이름` : package update

`npm uninstall  패키지이름` : 패키지 삭제
