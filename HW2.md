<h1>HW1</h1>
    
```swift


import SwiftUI

struct ContentView: View {
    @State private var playerScore = 0
    @State private var computerScore = 0
    @State private var roundResult = ""
    @State private var computerMove = ""
    @State private var isComputerMoveDisplayed = false
    @State private var isGameStarted = false
    @State private var isGameOver = false
    @State private var showWinImage = false
    @State private var showLoseImage = false
    
    let moves = ["Rock", "Paper", "Scissors"]
    
    var body: some View {
        VStack {
            Text("Rock, Paper, Scissors")
                .font(.title)
                .padding()
            
            Text("Player: \(playerScore) - Computer: \(computerScore)")
                .font(.headline)
                .padding()
            
            Text(roundResult)
                .font(.headline)
                .padding()
            
            if isGameStarted && !isGameOver {
                HStack {
                    ForEach(moves, id: \.self) { move in
                        Button(action: {
                            playRound(move)
                        }) {
                            VStack {
                                Image(move)
                                    .resizable()
                                    .frame(width: 100, height: 100)
                                
                                Text(move)
                                    .font(.headline)
                            }
                        }
                    }
                }
            }
            
            if isGameOver {
                VStack {
                    if showWinImage {
                        Image("Cheers")
                            .resizable()
                            .frame(width: 300, height: 250)
                            .padding()
                        Text("You Win!")
                    } else if showLoseImage {
                        Image("Emotional Damage")
                            .resizable()
                            .frame(width: 300, height: 250)
                            .padding()
                        Text("You Lose!")
                    } else {
                        Image("Try")
                            .resizable()
                            .frame(width: 300, height: 250)
                            .padding()
                        Text("It's a Tie!")
                    }
                    Button(action: {
                        resetGame()
                    }) {
                        Text("Try Again")
                            .padding()
                            .background(Color.red)
                            .foregroundColor(.white)
                            .cornerRadius(10)
                    }
                }
            } else {
                Button(action: {
                    isGameStarted.toggle()
                }) {
                    Text("Start")
                        .padding()
                        .background(Color.blue)
                        .foregroundColor(.white)
                        .cornerRadius(10)
                }
            }
        }
        .onAppear {
            if isGameStarted && !isGameOver {
                startAnimation()
            }
        }
    }
    
    func startAnimation() {
        _ = Timer.scheduledTimer(withTimeInterval: 0.2, repeats: true) { timer in
            computerMove = moves.randomElement() ?? "Rock"
            if isGameOver {
                timer.invalidate()
            }
        }
    }
    
    func playRound(_ playerMove: String) {
        if !isGameOver {
            isComputerMoveDisplayed = true
            isGameOver = true
            
            computerMove = moves.randomElement() ?? "Rock"
            roundResult = "Computer chose \(computerMove)"
            
            if playerMove == computerMove {
                roundResult += "\nIt's a tie!"
            } else if (playerMove == "Rock" && computerMove == "Scissors") ||
                        (playerMove == "Paper" && computerMove == "Rock") ||
                        (playerMove == "Scissors" && computerMove == "Paper") {
                roundResult += "\nYou win this round!"
                playerScore += 1
                showWinImage = true
                showLoseImage = false
            } else {
                roundResult += "\nComputer wins this round!"
                computerScore += 1
                showLoseImage = true
                showWinImage = false
            }
        }
    }
    
    func resetGame() {
        isGameStarted = false
        isGameOver = false
        roundResult = ""
        isComputerMoveDisplayed = false
        showWinImage = false
        showLoseImage = false
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}

    
```
(https://youtube.com/shorts/lYQz3kTgE80)
