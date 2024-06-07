# jpa

## 연관관계 (Association)
###  Item 1 : @OneToMany
- 외래 키 열을 영속성 컨텍스트와 동기화하는 것은 @ManyToOne 연결이 담당한다.
- 단방향 @OneToMany보다는 양방향 @OneToMany를 사용하자
- 부모 사이드에서 `mappedBy`, `orphanRemoval` 선언하기
  ~~~Java
  @OneToMany(cascade = CascadeType.ALL,
              mappedBy = "author",
              orphanRemoval = true) 
  ~~~
- helper method만들기 (부모측)
    ~~~java
    public void addBook(Book book) { 
        this.books.add(book); 
        book.setAuthor(this);
    }
    
    public void removeBook(Book book) { 
        book.setAuthor(null); 
        this.books.remove(book);
    }
  
- equals() and hashCode()는 자식 측에 선언한다. (다시 공부)
- @OneToMany는 기본적으로 LazyLoading이지만, @ManyToOne은 EagerLoading이다. -> 모두 LazyLoading을 사용하자. 
  `@ManyToOne(fetch = FetchType.LAZY)`

- toString()을 재정의하는 경우 데이터베이스에서 엔티티를 도르할 때 가져온 기본 속성만 포함하도록 하자.
  - 지연 속성이나 연관을 포함하면 해당 데이터를 가져오는 별도의 SQL문이 트리거되거나 LazyInitializationException이 발생한다.

[ 전체 코드 ]
~~~Java
@Entity
public class Book implements Serializable {
    private static final long serialVersionUID = 1L;
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String title;
    private String isbn;
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "author_id")
    private Author author;
    
    // getters and setters omitted for brevity
    @Override
    public boolean equals(Object obj) {
        if(obj == null) {
            return false;
        }
        
        if (this == obj) {
            return true;
        }
        
        if (getClass() != obj.getClass()) {
            return false;
        }
  
        return id != null && id.equals(((Book) obj).id);
    }
    
    @Override
    public int hashCode() {
        return 2021;
    }
    
    @Override
    public String toString() {
         return "Book{" + "id=" + id + ", title=" + title
                                + ", isbn=" + isbn + '}';
    } 
}

~~~