# jpa

## 연관관계 (Association)
###  Item 1 : @OneToMany
- 외래 키 열을 지속성 컨텍스트(퍼스트 레벨 캐시)와 동기화하는 것은 @ManyToOne 연결이 담당한다.
- 단방향 @OneToMany보다는 양방향 @OneToMany를 사용하자
- 부모의 생성이 자식에게 종속된다는 것은 말이 안 된다.
- 부모 사이드에서 mappedBy 선언하기
- 부모 사이드에 orphanRemoval 선언하기
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