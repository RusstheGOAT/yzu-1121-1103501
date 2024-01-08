<h1>hw4</h1>
<table>
   <tr>
      <td>
         
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            TabView{
                Group{
                    WelcomeView()
                        .tabItem { 
                            Image(systemName: "rosette")
                            Text("Home")
                        }
                    MovieView()
                        .tabItem { 
                            Image(systemName: "list.bullet")
                            Text("Movies")
                        }
                    externalView()
                        .tabItem { 
                            Image(systemName: "link")
                            Text("Links")
                        }
                    SettingView()
                        .tabItem { 
                            Image(systemName: "wrench.adjustable")
                            Text("Settings")
                        }
                }
            }
        }.padding(.top, 20)
            .tint(Color.white)
            .onAppear(perform: {
                UITabBar.appearance().backgroundColor = UIColor(Color.black) 
                UITabBar.appearance().unselectedItemTintColor = UIColor(Color.gray)
            })
            .frame(minWidth: 0, maxWidth: .infinity, minHeight: 0, maxHeight: .infinity)
            .background(Color.clear)
    }
}

```
   </tr>
</table>
<table>
   <tr>
      <td>
         
```swift
import SwiftUI

struct WelcomeView: View {
    var body: some View {
        VStack {
            HStack{
                VStack{
                    Text("PREPARE TO\nEXPERIENCE ")
                        .fontWeight(.bold)
                        .padding(8)
                        .lineSpacing(6.0)
                        .font(.title)
                    Text("LIFE AS YOU'VE NEVER SEEN IT.\nEMOTION AS YOU'VE NEVER HEARD IT.")
                        .fontWeight(.semibold)
                        .padding(8)
                        .lineSpacing(6.0)
                        .font(.subheadline)
                    
                }.padding(.trailing, 15)
                
            }
            Text("\"My precious.\"")
                .italic(true)
                .fontWeight(.bold)
                .font(.system(size: 15))
                .foregroundColor(.gray.opacity(0.8))
                .padding()
            HStack{
                Text("-The Lord of the Rings: Two Towers, 2002")
                    .font(.system(size: 10, weight: .regular, design: .default))
                    .foregroundColor(Color.gray)
                    .frame(width: 270, alignment: .trailing)
            }
        }
    }
}

```
   </tr>
</table>
<table>
   <tr>
      <td>
         
```swift
import SwiftUI

// Movie model with correctly cased and named properties
struct Movie: Identifiable {
    let id = UUID()
    let image: String
    let Intro: String
    let MovieTitle: String
    let ReleaseDate: String
    let Trailer: String
}

// Sample data array renamed to avoid conflict with struct Movie
let movies = [
    Movie(image: "Oppenheimer", Intro: "The story of American scientist J. Robert Oppenheimer and his role in the development of the atomic bomb.", MovieTitle: "Oppenheimer", ReleaseDate: "2023/07/21", Trailer: "https://www.youtube.com/watch?v=bK6ldnjE3Y0"),
    Movie(image: "Sound of Freedom", Intro: "The incredible true story of a former government agent turned vigilante who embarks on a dangerous mission to rescue hundreds of children from traffickers.", MovieTitle: "Sound of Freedom", ReleaseDate: "2023/09/22", Trailer: "https://www.youtube.com/watch?v=UwSBQWI-bek"),
    Movie(image: "Taylor Swift: The Eras Tour", Intro: "Experience the Eras Tour concert, performed by the one and only Taylor Swift.", MovieTitle: "Taylor Swift: The Eras Tour", ReleaseDate: "2023/11/03", Trailer: "https://www.youtube.com/watch?v=KudedLV0tP0"),
    Movie(image: "The Flash", Intro: "Barry Allen uses his super speed to change the past, but his attempt to save his family creates a world without super heroes, forcing him to race for his life in order to save the future.", MovieTitle: "The Flash", ReleaseDate: "2023/06/14", Trailer: "https://www.youtube.com/watch?v=hebWYacbdvc"),
    Movie(image: "Dungeons & Dragons: Honor Among Thieves", Intro: "A charming thief and a band of unlikely adventurers embark on an epic quest to retrieve a lost relic, but things go dangerously awry when they run afoul of the wrong people.", MovieTitle: "Dungeons & Dragons: Honor Among Thieves", ReleaseDate: "2023/03/29", Trailer: "https://www.youtube.com/watch?v=IiMinixSXII"),
    Movie(image: "Killers of the Flower Moon", Intro: "When oil is discovered in 1920s Oklahoma under Osage Nation land, the Osage people are murdered one by one - until the FBI steps in to unravel the mystery.", MovieTitle: "Killers of the Flower Moon", ReleaseDate: "2023/10/20", Trailer: "https://www.youtube.com/watch?v=EP34Yoxs3FQ"),   
    Movie(image: "Gran Turismo", Intro: "Based on the unbelievable, inspiring true story of a team of underdogs - a struggling, working-class gamer, a failed former race car driver, and an idealistic motorsport exec - who risk it all to take on the most elite sport in the world.", MovieTitle: "Gran Turismo", ReleaseDate: "2023/08/23", Trailer: "https://www.youtube.com/watch?v=GVPzGBvPrzw"),
    Movie(image: "Everything Everywhere All at Once", Intro: "A middle-aged Chinese immigrant is swept up into an insane adventure in which she alone can save existence by exploring other universes and connecting with the lives she could have led.", MovieTitle: "Everything Everywhere All at Once", ReleaseDate: "2022/04/22", Trailer: "https://www.youtube.com/watch?v=wxN1T1uxQ2g"),
    Movie(image: "The Fabelmans", Intro: "Growing up in post-World War II era Arizona, young Sammy Fabelman aspires to become a filmmaker as he reaches adolescence, but soon discovers a shattering family secret and explores how the power of films can help him see the truth.", MovieTitle: "The Fabelmans", ReleaseDate: "2023/02/24", Trailer: "https://www.youtube.com/watch?v=D1G2iLSzOe8"),
]

// Renamed MovieView to MoviesListView for clarity
struct MovieView: View {
    @State private var showingDetail = false
    @State private var selectedMovie: Movie?
    
    var body: some View {
        NavigationView {
            List(movies) { movie in
                BasicImageRow(movie: movie)
                    .onTapGesture {
                        self.showingDetail = true
                        self.selectedMovie = movie
                    }
            }
            .sheet(isPresented: $showingDetail) {
                if let selectedMovie = selectedMovie {
                    MovieDetailView(movie: selectedMovie)
                }
            }
            .navigationTitle("Movies")
        }
    }
}

struct BasicImageRow: View {
    var movie: Movie
    var body: some View {
        HStack {
            Image(movie.image)
                .resizable()
                .frame(width: 40, height: 40)
                .cornerRadius(5)
            Text(movie.MovieTitle)
        }
    }
}

struct MovieDetailView: View {
    @Environment(\.presentationMode) var presentationMode
    var movie: Movie
    
    var body: some View {
        ScrollView {
            VStack {
                MoviePoster(image: movie.image)
                MovieMovieTitle(MovieTitle: movie.MovieTitle)
                MovieReleaseDate(date: movie.ReleaseDate)
                MovieIntro(Intro: movie.Intro)
                MovieTrailerLink(Trailer: movie.Trailer)
            }
        }
        .overlay(DismissButton())
    }
}

// Decomposed views for MovieDetailView
struct MoviePoster: View {
    let image: String
    var body: some View {
        Image(image)
            .resizable()
            .aspectRatio(contentMode: .fill)
            .clipped()
    }
}

struct MovieMovieTitle: View {
    let MovieTitle: String
    var body: some View {
        Text(MovieTitle)
            .font(.system(.title))
            .fontWeight(.black)
    }
}

struct MovieReleaseDate: View {
    let date: String
    var body: some View {
        Text("Release Date: \(date)")
            .font(.caption)
        Spacer()
    }
}

struct MovieIntro: View {
    let Intro: String
    var body: some View {
        Text(Intro)
            .padding()
            .background(Color.gray)
            .cornerRadius(10)
           // .opacity(0.3)
            .frame(maxWidth: 350)
    }
}

struct MovieTrailerLink: View {
    let Trailer: String
    var body: some View {
        Link("Trailer", destination: URL(string: Trailer)!)
            .padding()
            .frame(width: 110, height: 45)
            .background(LinearGradient(gradient: Gradient(colors: [Color(red: 197/255, green: 149/255, blue: 217/255), Color(red: 58/255, green: 13/255, blue: 93/255)]), startPoint: .leading, endPoint: .trailing))
            .foregroundColor(.white)
            .font(.system(size: 20, design: .serif))
            .cornerRadius(30)
    }
}

struct dismissbutton: View {
    @Environment(\.presentationMode) var presentationMode
    
    var body: some View {
        Button(action: {
            self.presentationMode.wrappedValue.dismiss()
        }) {
            Image(systemName: "chevron.down.circle.fill")
                .font(.largeTitle)
                .foregroundColor(.white)
                .padding(.top, 600)
        }
    }
}

```
   </tr>
</table>
<table>
   <tr>
      <td>

```swift
import SwiftUI

struct Course: Identifiable {
    let id = UUID()
    let image: String
    let title: String
    let externalLink: String
}

let courses = [
    Course(image: "IMDb", title: "IMDb", externalLink: "https://www.imdb.com/"),
    Course(image: "RottenTomatoes",  title: "RottenTomatoes", externalLink: "https://www.rottentomatoes.com/"),
    Course(image: "Box Office",  title: "BoxOffice", externalLink: "https://www.boxofficemojo.com/"),
]

struct externalView: View {
    @State private var showingDetailView = false
    @State private var selectedCourse: Course?
    
    var body: some View {
        VStack {
            HeaderView(title: "External Links")
            ScrollView(.horizontal, showsIndicators: false) {
                HStack {
                    ForEach(courses) { course in
                        CourseCard(course: course)
                            .onTapGesture {
                                self.showingDetailView = true
                                self.selectedCourse = course
                            }
                    }
                }
            }
            .sheet(isPresented: $showingDetailView) {
                if let selectedCourse = selectedCourse {
                    CourseDetailView(course: selectedCourse)
                }
            }
        }
    }
}

struct HeaderView: View {
    let title: String
    
    var body: some View {
        Text(title)
            .padding(.top, 20)
            .font(.largeTitle)
            .foregroundStyle(.white)
    }
}

struct CourseCard: View {
    var course: Course
    
    var body: some View {
        VStack {
            Image(course.image)
                .resizable()
                .aspectRatio(contentMode: .fit)
            Text(course.title)
                .font(.title)
                .foregroundStyle(.primary)
                .lineLimit(3)
                .frame(maxWidth: .infinity)
                .padding()
        }
        .background(Color(.systemGray5))
        .cornerRadius(20)
        .overlay(RoundedRectangle(cornerRadius: 20).stroke(Color.gray, lineWidth: 2))
        .padding()
    }
}

struct CourseDetailView: View {
    @Environment(\.presentationMode) var presentationMode
    var course: Course
    
    var body: some View {
        ScrollView {
            VStack {
                CourseImage(image: course.image)
                CourseTitle(title: course.title)
                ExternalLinkButton(link: course.externalLink)
            }
        }
        .overlay(DismissButton())
    }
}

struct CourseImage: View {
    let image: String
    
    var body: some View {
        Image(image)
            .resizable()
            .aspectRatio(contentMode: .fill)
            .clipped()
    }
}

struct CourseTitle: View {
    let title: String
    
    var body: some View {
        Text(title)
            .font(.system(.title))
            .fontWeight(.black)
    }
}

struct ExternalLinkButton: View {
    let link: String
    
    var body: some View {
        Link("link", destination: URL(string: link)!)
            .padding()
            .frame(width: 110, height: 45)
            .background(LinearGradient(gradient: Gradient(colors: [Color(red: 197/255, green: 149/255, blue: 217/255), Color(red: 58/255, green: 13/255, blue: 93/255)]), startPoint: .leading, endPoint: .trailing))
            .foregroundColor(.white)
            .font(.system(size: 20, design: .serif))
            .cornerRadius(20)
    }
}

struct DismissButton: View {
    @Environment(\.presentationMode) var presentationMode
    
    var body: some View {
        Button(action: {
            self.presentationMode.wrappedValue.dismiss()
        }) {
            Image(systemName: "chevron.down.circle.fill")
                .font(.largeTitle)
                .foregroundColor(.white)
        }
        .padding(.trailing, 20)
        .padding(.top, 30)
    }
}
```
   </tr>
</table>
<table>
   <tr>
      <td>

```swift
import SwiftUI

struct SettingView: View {
    let displayFontType = [".default",".rounded",".monospaced",".serif"]
    
    @State var displayFontSelected = 0
    @State var isDeepScheme = false
    @State var colorArray: [Double] = [255.0, 255.0, 255.0]
    @State var stepperValue = 0
    @State var sliderValue = 0.0
    @State var date = Date()
    @State private var selectedLanguage = "English" // Default language
    
    var body: some View {
        NavigationView {
            Form {
                Section(header: Text("Font Settings")) {
                    Picker("Select Font", selection: $displayFontSelected) {
                        ForEach(0..<displayFontType.count, id: \.self) {
                            Text(self.displayFontType[$0])
                        }
                    }
                }
                
                Section(header: Text("Background Style")) {
                    Toggle("Dark Mode \(String(isDeepScheme))", isOn: $isDeepScheme)
                }
                
                Section(header: Text("Counter")) {
                    Stepper(value: $stepperValue) {
                        Text("Stepper \(stepperValue)")
                    }
                }
                
                Section(header: Text("Slider \(sliderValue, specifier: "%.2f")")) {
                    Slider(value: $sliderValue, in: 0...1)
                }
                
                Section(header: Text("Date")) {
                    DatePicker("date", selection: $date, displayedComponents: [.date])
                }
                
                Section(header: Text("Language")) {
                    Picker("Select Language", selection: $selectedLanguage) {
                        Text("English").tag("English")
                        Text("中文").tag("Chinese")
                    }
                }
            }
            .navigationTitle("Settings")
        }
    }
}
```
   </tr>
</table>
[微型作業4demo](https://youtube.com/shorts/lYQz3kTgE80](https://youtu.be/Ac2H4Aq185c)https://youtu.be/Ac2H4Aq185c)
