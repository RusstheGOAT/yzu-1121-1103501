<h1>HW1</h1>
    
```swift

    import SwiftUI
    import PlaygroundSupport

struct ContentView: View {
    var body: some View {
        ZStack {
            Color(.systemGray6)
            Text("Basic Info")
                .font(.largeTitle)
                .foregroundColor(.primary)
                .underline()
                .position(x: 100, y: 102) // Adjust position to move to the top-left corner
            Image("Photo")
                .resizable()
                .frame(width: 150, height: 150)
                .clipShape(Circle())
                .overlay(Circle().stroke(Color.white, lineWidth: 4))
                .position(x: 275, y: 105) 
            VStack(alignment: .leading, spacing: 10) {
                Text("Student Number: 1103501")
                    .font(.headline)
                    .foregroundColor(.primary)
                Text("Name: Evan Shiao")
                    .font(.headline)
                    .foregroundColor(.primary)
                Text("Static hobbys: photography, drawing,\n    watching films, ramen lover.")
                    .font(.headline)
                    .foregroundColor(.primary)
                Text("Dynamic hobbys: Mountaineering,\n    backpacking, running.")
                    .font(.headline)
                    .foregroundColor(.primary)              
            }
            Image(systemName: "scribble.variable")
                .font(.system(size : 100))
                .position(x: 190, y: 480)
            
            
            Text("MANNERS. MAKETH. MAN.")
                .font(.title2)
                .fontWeight(.heavy)
                .foregroundColor(.primary)
                .position(x: 190, y:600)
        }
    }
}


    
```

<img width="40%"  src="https://github.com/RusstheGOAT/yzu-1121-1103501/blob/main/homework1.jpg">
