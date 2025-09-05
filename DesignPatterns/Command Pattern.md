# 명령 패턴 #
사용자의 명령을 객체로 캡슐화 -> 실행될 명령을 매개변수화, 저장, 취소, 다시실행을 할 수 있게 하는 패턴
### 장점 ###
- 명령 처리와 행동 로직을 분리 (유지보수)
- Undo/Redo 구현이 쉬움
- 명령들을 큐에 저장하거나, 네트워크로 전송하거나 스크립팅에도 활용 가능
### 단점 ###
- 클래스가 많이 늘어남 (각 명령마다 새로운 클래스 필요)
- 간단한 상황에선 오히려 과도함
---
## 예제 ##
플레이어가 점프,공격을 할 수 있다고 가정
```
class Player {
public:
    void jump() { cout << "Player jumps!\n"; }
    void attack() { cout << "Player attacks!\n"; }
};
```
---
명령의 객체화를 위한 추상클래스
```
class Command {
public:
    virtual void execute() = 0;
    virtual void undo() = 0;
    virtual ~Command() {}
};
```
---
실제 명령 클래스
```
class JumpCommand : public Command {
    Player* player;
public:
    JumpCommand(Player* p) : player(p) {}
    void execute() override { player->jump(); }
    void undo() override { cout << "Undo jump.\n"; }
};

class AttackCommand : public Command {
    Player* player;
public:
    AttackCommand(Player* p) : player(p) {}
    void execute() override { player->attack(); }
    void undo() override { cout << "Undo attack.\n"; }
};
```
---
InputHandler
```
class InputHandler {
    map<char, Command*> commandMap;
    stack<Command*> history;  // Undo 용도

public:
    void bindCommand(char key, Command* command) {
        commandMap[key] = command;
    }

    void handleInput(char input) {
        if (commandMap.find(input) != commandMap.end()) {
            Command* cmd = commandMap[input];
            cmd->execute();
            history.push(cmd);
        }
    }

    void undoLast() {
        if (!history.empty()) {
            Command* last = history.top();
            last->undo();
            history.pop();
        }
    }
};
```
---
실행 부분
```
int main() {
    Player player;

    // 명령 생성
    JumpCommand jump(&player);
    AttackCommand attack(&player);

    // 입력 핸들러에 키 바인딩
    InputHandler inputHandler;
    inputHandler.bindCommand('j', &jump);
    inputHandler.bindCommand('a', &attack);

    // 가상의 키 입력 시나리오
    string inputSequence = "ja";

    for (char key : inputSequence) {
        inputHandler.handleInput(key);  // 명령 실행
    }

    // 실행 취소
    cout << "--- Undo last command ---\n";
    inputHandler.undoLast();
}
```
---


