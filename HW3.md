<h1>HW1</h1>
    
```swift

import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            TitleView()
            Text("\nMUSIC")
            MaleAlbum()
                .padding()
                .background(Color.brown)
            FemaleAlbum()
                .padding()
                .background(Color.red)
            Text("MUVIE")
            WarMovie()
            AnimationMovie()
        }
    }
}
struct TitleView: View{
    var body: some View{
        VStack(alignment: .center, spacing: 2) {
            Text("\nmusic&movie Collection")
                .font(.title)
                .fontWeight(.bold)
                .font(.system(size:30))
                .foregroundColor(Color(.white))
        }
    }
}
struct FemaleAlbum: View {
    var body: some View {
        VStack{
            HStack{
                Image("Red")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Text("Taylor Swift - Red")
                    .fontWeight(.semibold)
                    .font(.system(size:10))
                Image("Reputation")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Text("Talor Swift - Reputation")
                    .fontWeight(.semibold)
                    .font(.system(size:10))
                Image("1989")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Text("Taylor Swift - 1989")
                    .fontWeight(.semibold)
                    .font(.system(size:10))
            }
        }
    }
}
struct MaleAlbum: View {
    var body: some View {
        VStack{
            HStack{
                Image("Up all night")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Text("One direction - Up all night")
                    .fontWeight(.semibold)
                    .font(.system(size:10))
                Image("Take me home")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Text("One direction - Take me home")
                    .fontWeight(.semibold)
                    .font(.system(size:10))
                Image("Midnight memories")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Text("One direction - Midnight memories")
                    .fontWeight(.semibold)
                    .font(.system(size:10 ))
            }
            HStack{
                Image("How I am feeling")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Text("LAUV - How I'm feeling")
                    .fontWeight(.semibold)
                    .font(.system(size:10))
                Image("All 4 nothing")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Text("LAUV - All 4 nothing")
                    .fontWeight(.semibold)
                    .font(.system(size:10))
            }
        }
    }
}
struct AnimationMovie: View {
    var body: some View{
        VStack{
            Image("Spider-man")
                .resizable()
                .aspectRatio(contentMode: .fit)
            Text("SPIDER-MAN ACROSS THE SPIDER VERSE")
                .fontWeight(.medium)
                .font(.system(size:10))
        }
    }
}
struct WarMovie: View{
    var body: some View{
        VStack{
            HStack{
                Image("1917")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Image("Dunkirk")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
            }
            HStack{
                Text("1917                                                      ")
                    .fontWeight(.medium)
                    .font(.system(size:10))
                Text("DUNKIRK")
                    .fontWeight(.medium)
                    .font(.system(size:10))
            }
        }
    }
}


    
```

<img width="40%"  src="https://github.com/RusstheGOAT/yzu-1121-1103501/blob/main/homework3.jpg">
