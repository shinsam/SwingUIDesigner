# SwingUIDesigner

🧾 SwingUIDesigner 프로젝트 설명서
📌 개요
SwingUIDesigner는 Java Swing을 기반으로 하는 비주얼 UI 디자인 툴입니다. 사용자는 마우스를 이용해 컴포넌트를 배치하고 속성을 설정한 뒤, 그 결과를 실행 가능한 Java 코드로 저장할 수 있습니다. 비전문 개발자도 직관적으로 GUI를 구성할 수 있도록 돕는 도구입니다.

🖥️ 화면 구성
구역	설명
좌측 디자인 영역	컴포넌트를 배치하고 수정할 수 있는 영역. 50픽셀 단위의 격자 표시 및 실시간 마우스 좌표 출력 포함
우측 미리보기 영역	구성된 UI를 실시간으로 반영하여 미리 확인 가능 (드래그/수정 불가)
하단 버튼	코드 내보내기 및 파일 저장 버튼

🧩 주요 기능 요약
1. 컴포넌트 추가
디자인 영역을 더블클릭하면 설정 다이얼로그가 표시됨

지원되는 컴포넌트 종류:

JButton

JCheckBox

JRadioButton (라디오 그룹 가능)

JLabel (TextView 역할)

속성 설정 항목:

텍스트 (기본값: 자동 생성된 컴포넌트 ID)

폰트 크기

크기 (width, height)

색상 (JColorChooser로 선택)

JRadioButton의 경우 그룹 ID 설정 가능

2. 컴포넌트 위치 조정
컴포넌트는 드래그를 통해 디자인 패널 내에서 자유롭게 위치 이동 가능

이동된 위치는 자동으로 저장 코드에 반영됨 (getX(), getY() 활용)

3. 자동 컴포넌트 이름 생성
생성되는 모든 컴포넌트는 타입 기반으로 고유 ID 자동 부여

예: button1, radio2, label3

이 이름은 실제 Java 코드 내 변수명으로 사용되며, UI상 텍스트 기본값으로도 사용됨

4. 라디오 버튼 그룹 설정
JRadioButton은 동일한 그룹 ID를 갖는 버튼끼리 ButtonGroup으로 묶임

동시에 하나만 선택 가능

그룹 정보는 코드에도 자동 반영됨

java
Copy
Edit
Map<String, ButtonGroup> groupMap = new HashMap<>();
groupMap.computeIfAbsent("group1", k -> new ButtonGroup()).add(radio1);
5. 컴포넌트 선택 및 삭제
마우스로 클릭 시 선택 테두리(빨간색) 표시

선택된 상태에서 Delete 키를 누르면 해당 컴포넌트 삭제

6. 실시간 마우스 좌표 표시
디자인 패널 좌측 상단에 JLabel을 표시하여 마우스 좌표를 실시간 출력

해당 라벨은 JLayeredPane을 사용해 designPanel 위에 독립적으로 겹쳐서 표시

7. 50px 단위 그리드 표시
디자인 영역 배경에 연한 회색 선으로 50픽셀 단위 격자 표시

컴포넌트 정렬 및 배치 시 가이드 역할 수행

8. 코드 내보내기 및 저장
“코드 내보내기”: 콘솔에 Java 코드 출력

“저장하기”: 사용자 지정 위치에 .java 파일로 저장 (JFileChooser)

저장되는 코드는 전체 UI 구성을 포함한 실행 가능한 Java Swing 프로그램 형태

📁 저장되는 Java 파일 구조 예시
java
Copy
Edit
public class GuiCode {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Generated UI");
        JPanel panel = new JPanel(null);
        Map<String, ButtonGroup> groupMap = new HashMap<>();

        JButton button1 = new JButton("button1");
        button1.setBounds(50, 100, 120, 30);
        panel.add(button1);

        JRadioButton radio1 = new JRadioButton("radio1");
        radio1.setBounds(200, 100, 120, 30);
        panel.add(radio1);
        groupMap.computeIfAbsent("group1", k -> new ButtonGroup()).add(radio1);

        frame.add(panel);
        frame.setVisible(true);
    }
}
🧱 기술 요소 요약
기술 요소	사용 목적
JPanel	UI 영역 분리 및 컴포넌트 배치
JLayeredPane	좌표 라벨을 겹쳐서 표시
MouseListener / MouseMotionListener	클릭, 이동, 드래그 처리
ButtonGroup	라디오 버튼 그룹 관리
JFileChooser	사용자 지정 위치에 파일 저장
null layout	절대 좌표 기반 배치
paintComponent()	격자 표시

🧠 추천 확장 기능 (향후 발전 방향)
기능 제안	설명
저장된 구성 불러오기	JSON 등으로 저장 후 다시 로딩 가능
Undo/Redo	사용자 액션을 기록하여 되돌리기 지원
Snap-to-grid	컴포넌트 위치 자동 정렬
속성 편집 기능	이미 생성된 컴포넌트를 더블클릭하여 속성 수정
레이아웃 기반 설계 지원	BorderLayout, GridLayout 등 논리 배치 도입

