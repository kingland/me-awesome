### Overview
we are going to learn about Unit Testing Spring Boot application using Junit 5 and we will see how to use Mocking frameworks like Mockito.

### Install
Maven
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.6.2</version>
    <scope>test</scope>
</dependency>
```

***spring-boot-starter-test*** library, you can see that it includes ***Junit 4*** as a transitive dependency

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
    <exclusions>
        <exclusion>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

```xml
<build>
    <plugins>
        <plugin>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.22.2</version>
        </plugin>
        <plugin>
            <artifactId>maven-failsafe-plugin</artifactId>
            <version>2.22.2</version>
        </plugin>
    </plugins>
</build>
```

### Command

```shell
# Run all the unit test classes.
$ mvn test

# Run a single test class.
$ mvn -Dtest=TestApp1 test

# Run multiple test classes.
$ mvn -Dtest=TestApp1,TestApp2 test

# Run a single test method from a test class.
$ mvn -Dtest=TestApp1#methodname test

# Run all test methods that match pattern 'testHello*' from a test class.
$ mvn -Dtest=TestApp1#testHello* test

# Run all test methods match pattern 'testHello*' and 'testMagic*' from a test class.
$ mvn -Dtest=TestApp1#testHello*+testMagic* test
```

### JUnit Assertion
```java
public class Assertions {
    public static void assertAll​(String heading, Collection<Executable> executables);
    public static void assertAll​(String heading, Stream<Executable> executables);
    public static void assertAll​(String heading, Executable... executables);
    public static void assertAll​(Collection<Executable> executables);
    public static void assertAll​(Stream<Executable> executables);
    public static void assertAll​(Executable... executables);

    //E,A= boolean, byte, char, int, long, short, Object
    public static void assertArrayEquals​(E[] expected, A[] actual);
    public static void assertArrayEquals​(E[] expected, A[] actual, String message);
    public static void assertArrayEquals​(E[] expected, A[] actual, Supplier<String> messageSupplier);

    //E,A,D = double, float
    public static void assertArrayEquals​(E[] expected, A[] actual);
    public static void assertArrayEquals​(E[] expected, A[] actual, D delta);
    public static void assertArrayEquals​(E[] expected, A[] actual, D delta, String message);
    public static void assertArrayEquals​(E[] expected, A[] actual, D delta, Supplier<String> messageSupplier);
    public static void assertArrayEquals​(E[] expected, A[] actual, String message);
    public static void assertArrayEquals​(E[] expected, A[] actual, Supplier<String> messageSupplier);

    public static void assertDoesNotThrow​(Executable executable);
    public static void assertDoesNotThrow​(Executable executable, String message);
    public static void assertDoesNotThrow​(Executable executable, Supplier<String> messageSupplier);
    public static <T> T assertDoesNotThrow​(ThrowingSupplier<T> supplier);
    public static <T> T assertDoesNotThrow​(ThrowingSupplier<T> supplier, String message);
    public static <T> T assertDoesNotThrow​(ThrowingSupplier<T> supplier, Supplier<String> messageSupplier);
    
    // E = byte,      char, int,         long,      short,       byte,      Character
    // A = byte/Byte, char, int/Integer, long/Long, short/Short, byte/Byte, char/Character
    public static void assertEquals​(E expected, A actual);
    public static void assertEquals​(E expected, A actual, String message);
    public static void assertEquals​(E expected, A actual, Supplier<String> messageSupplier);
    public static void assertEquals​(E expected, A actual);
    public static void assertEquals​(E expected, A actual, String message);
    public static void assertEquals​(E expected, A actual, Supplier<String> messageSupplier);

    // E = double,        float
    // A = double/Double, float/Float
    // D = double,        float
    public static void assertEquals​(E expected, A actual);
    public static void assertEquals​(E expected, A actual, D delta);
    public static void assertEquals​(E expected, A actual, D delta, String message);
    public static void assertEquals​(E expected, A actual, D delta, Supplier<String> messageSupplier);
    public static void assertEquals​(E expected, A actual, String message);
    public static void assertEquals​(E expected, A actual, Supplier<String> messageSupplier);

    // E = Double,        Float,       Integer,     Long,      Object, Short
    // A = double/Double, flaot/Float, int/Integer, long/Long, Object, Short
    public static void assertEquals​(E expected, A actual);
    public static void assertEquals​(E expected, A actual, String message);
    public static void assertEquals​(E expected, A actual, Supplier<String> messageSupplier);

    public static void assertFalse​(boolean condition);
    public static void assertFalse​(boolean condition, String message);
    public static void assertFalse​(boolean condition, Supplier<String> messageSupplier);
    public static void assertFalse​(BooleanSupplier booleanSupplier);
    public static void assertFalse​(BooleanSupplier booleanSupplier, String message);
    public static void assertFalse​(BooleanSupplier booleanSupplier, Supplier<String> messageSupplier);

    public static <T> T assertInstanceOf​(Class<T> expectedType, Object actualValue);
    public static <T> T assertInstanceOf​(Class<T> expectedType, Object actualValue, String message);
    public static <T> T assertInstanceOf​(Class<T> expectedType, Object actualValue, Supplier<String> messageSupplier);

    public static void assertIterableEquals​(Iterable<?> expected, Iterable<?> actual);
    public static void assertIterableEquals​(Iterable<?> expected, Iterable<?> actual, String message);
    public static void assertIterableEquals​(Iterable<?> expected, Iterable<?> actual, Supplier<String> messageSupplier);
    public static void assertLinesMatch​(List<String> expectedLines, List<String> actualLines);
    public static void assertLinesMatch​(List<String> expectedLines, List<String> actualLines, String message);
    public static void assertLinesMatch​(List<String> expectedLines, List<String> actualLines, Supplier<String> messageSupplier);
    public static void assertLinesMatch​(Stream<String> expectedLines, Stream<String> actualLines);
    public static void assertLinesMatch​(Stream<String> expectedLines, Stream<String> actualLines, String message);
    public static void assertLinesMatch​(Stream<String> expectedLines, Stream<String> actualLines, Supplier<String> messageSupplier);

    // U = byte,      char,           int,         long,      short
    // A = byte/Byte, char/Cherecter, int/Integer, long/Long, short/Short
    public static void assertNotEquals​(U unexpected, A actual);
    public static void assertNotEquals​(U unexpected, A actual, String message);
    public static void assertNotEquals​(U unexpected, A actual, Supplier<String> messageSupplier);

    // E = double,        float
    // A = double/Double, float/Float
    // D = double,        float
    public static void assertNotEquals​(E unexpected, A actual);
    public static void assertNotEquals​(E unexpected, A actual, D delta);
    public static void assertNotEquals​(E unexpected, A actual, D delta, String message);
    public static void assertNotEquals​(E unexpected, A actual, D delta, Supplier<String> messageSupplier);
    public static void assertNotEquals​(E unexpected, A actual, String message);
    public static void assertNotEquals​(E unexpected, A actual, Supplier<String> messageSupplier);

    // E = Double,        Float,       Integer,     Long,      Object, Short
    // A = double/Double, flaot/Float, int/Integer, long/Long, Object, Short
    public static void assertNotEquals​(E expected, A actual);
    public static void assertNotEquals​(E expected, A actual, String message);
    public static void assertNotEquals​(E expected, A actual, Supplier<String> messageSupplier);

    // NotNull
    public static void assertNotNull​(Object actual);
    public static void assertNotNull​(Object actual, String message);
    public static void assertNotNull​(Object actual, Supplier<String> messageSupplier);
    public static void assertNotSame​(Object unexpected, Object actual);
    public static void assertNotSame​(Object unexpected, Object actual, String message);
    public static void assertNotSame​(Object unexpected, Object actual, Supplier<String> messageSupplier);

    // Null
    public static void assertNull​(Object actual);
    public static void assertNull​(Object actual, String message);
    public static void assertNull​(Object actual, Supplier<String> messageSupplier);
    public static void assertSame​(Object expected, Object actual);
    public static void assertSame​(Object expected, Object actual, String message);
    public static void assertSame​(Object expected, Object actual, Supplier<String> messageSupplier);

    //Throwable
    public static <T extends Throwable> T assertThrows​(Class<T> expectedType, Executable executable);
    public static <T extends Throwable> T assertThrows​(Class<T> expectedType, Executable executable, String message);
    public static <T extends Throwable> T assertThrows​(Class<T> expectedType, Executable executable, Supplier<String> messageSupplier);
    public static <T extends Throwable> T assertThrowsExactly​(Class<T> expectedType, Executable executable);
    public static <T extends Throwable> T assertThrowsExactly​(Class<T> expectedType, Executable executable, String message);
    public static <T extends Throwable> T assertThrowsExactly​(Class<T> expectedType, Executable executable, Supplier<String> messageSupplier);

    //Timeout
    public static void assertTimeout​(Duration timeout, Executable executable);
    public static void assertTimeout​(Duration timeout, Executable executable, String message);
    public static void assertTimeout​(Duration timeout, Executable executable, Supplier<String> messageSupplier);
    public static <T> T assertTimeout​(Duration timeout, ThrowingSupplier<T> supplier);
    public static <T> T assertTimeout​(Duration timeout, ThrowingSupplier<T> supplier, String message);
    public static <T> T assertTimeout​(Duration timeout, ThrowingSupplier<T> supplier, Supplier<String> messageSupplier);
    public static void assertTimeoutPreemptively​(Duration timeout, Executable executable);
    public static void assertTimeoutPreemptively​(Duration timeout, Executable executable, String message);
    public static void assertTimeoutPreemptively​(Duration timeout, Executable executable, Supplier<String> messageSupplier);
    public static <T> T assertTimeoutPreemptively​(Duration timeout, ThrowingSupplier<T> supplier);
    public static <T> T assertTimeoutPreemptively​(Duration timeout, ThrowingSupplier<T> supplier, String message);
    public static <T> T assertTimeoutPreemptively​(Duration timeout, ThrowingSupplier<T> supplier, Supplier<String> messageSupplier);

    //True/False
    public static void assertTrue​(boolean condition);
    public static void assertTrue​(boolean condition, String message);
    public static void assertTrue​(boolean condition, Supplier<String> messageSupplier);
    public static void assertTrue​(BooleanSupplier booleanSupplier);
    public static void assertTrue​(BooleanSupplier booleanSupplier, String message);
    public static void assertTrue​(BooleanSupplier booleanSupplier, Supplier<String> messageSupplier);

    //Fail
    public static <V> V fail();
    public static <V> V fail​(String message);
    public static <V> V fail​(String message, Throwable cause);
    public static <V> V fail​(Throwable cause);
    public static <V> V fail​(Supplier<String> messageSupplier);

}
```

### Basic
```java
@Test
@DisplayName("Test Should Pass When Comment do not Contains Swear Words")
public void shouldNotContainSwearWordsInsideComment() {
    CommentService commentService = new CommentService(null, null, null, null, null, null, null);
    assertThat(commentService.containsSwearWords("This is a comment")).isFalse();
}
```
```java
@Test
@DisplayName("Should Throw Exception when Exception Contains Swear Words")
public void shouldFailWhenCommentContainsSwearWords() {
    CommentService commentService = new CommentService(null, null, null, null, null, null, null);
 
    assertThatThrownBy(() -> {
        commentService.containsSwearWords("This is a shitty comment");
    }).isInstanceOf(SpringRedditException.class)
            .hasMessage("Comments contains unacceptable language");
}
```

### Service Layer

```java
import com.programming.techie.springredditclone.dto.PostResponse;
import com.programming.techie.springredditclone.mapper.PostMapper;
import com.programming.techie.springredditclone.model.Post;
import com.programming.techie.springredditclone.repository.PostRepository;
import com.programming.techie.springredditclone.repository.SubredditRepository;
import com.programming.techie.springredditclone.repository.UserRepository;
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;
 
import java.time.Instant;
import java.util.Optional;
 
class PostServiceTest {
 
    private PostRepository postRepository = Mockito.mock(PostRepository.class);
    private SubredditRepository subredditRepository = Mockito.mock(SubredditRepository.class);
    private UserRepository userRepository = Mockito.mock(UserRepository.class);
    private AuthService authService = Mockito.mock(AuthService.class);
    private PostMapper postMapper = Mockito.mock(PostMapper.class);
 
    @Test
    @DisplayName("Should Retrieve Post by Id")
    public void shouldFindPostById() {
 
        PostService postService = new PostService(postRepository, subredditRepository, userRepository, authService, postMapper);
 
        Post post = new Post(123L, "First Post", "http://url.site", "Test",
                0, null, Instant.now(), null);
        PostResponse expectedPostResponse = new PostResponse(123L, "First Post", "http://url.site", "Test",
                "Test User", "Test Subredit", 0, 0, "1 Hour Ago", false, false);
 
        Mockito.when(postRepository.findById(123L)).thenReturn(Optional.of(post));
        Mockito.when(postMapper.mapToDto(Mockito.any(Post.class))).thenReturn(expectedPostResponse);
 
        PostResponse actualPostResponse = postService.getPost(123L);
 
        Assertions.assertThat(actualPostResponse.getId()).isEqualTo(expectedPostResponse.getId());
        Assertions.assertThat(actualPostResponse.getPostName()).isEqualTo(expectedPostResponse.getPostName());
    }

    @Test
    @DisplayName("Should Save Posts")
    public void shouldSavePosts() {
        PostService postService = new PostService(postRepository, subredditRepository, userRepository, authService, postMapper);
    
        User currentUser = new User(123L, "test user", "secret password", "user@email.com", Instant.now(), true);
        Subreddit subreddit = new Subreddit(123L, "First Subreddit", "Subreddit Description", emptyList(), Instant.now(), currentUser);
        Post post = new Post(123L, "First Post", "http://url.site", "Test",
                0, null, Instant.now(), null);
        PostRequest postRequest = new PostRequest(null, "First Subreddit", "First Post", "http://url.site", "Test");
    
        Mockito.when(subredditRepository.findByName("First Subreddit"))
                .thenReturn(Optional.of(subreddit));
        Mockito.when(postMapper.map(postRequest, subreddit, currentUser))
                .thenReturn(post);
        postService.save(postRequest);
        Mockito.verify(postRepository, Mockito.times(1)).save(ArgumentMatchers.any(Post.class));
    
    }
}
```
Using @Mock annotations

```java
import com.programming.techie.springredditclone.dto.PostResponse;
import com.programming.techie.springredditclone.mapper.PostMapper;
import com.programming.techie.springredditclone.model.Post;
import com.programming.techie.springredditclone.repository.PostRepository;
import com.programming.techie.springredditclone.repository.SubredditRepository;
import com.programming.techie.springredditclone.repository.UserRepository;
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.junit.jupiter.MockitoExtension;
 
import java.time.Instant;
import java.util.Optional;
 
@ExtendWith(MockitoExtension.class)
class PostServiceTest {
 
    @Mock
    private PostRepository postRepository;
    @Mock
    private SubredditRepository subredditRepository;
    @Mock
    private UserRepository userRepository;
    @Mock
    private AuthService authService;
    @Mock
    private PostMapper postMapper;
 
    @Test
    @DisplayName("Should Retrieve Post by Id")
    public void shouldFindPostById() {
 
        PostService postService = new PostService(postRepository, subredditRepository, userRepository, authService, postMapper);
 
        Post post = new Post(123L, "First Post", "http://url.site", "Test",
                0, null, Instant.now(), null);
        PostResponse expectedPostResponse = new PostResponse(123L, "First Post", "http://url.site", "Test",
                "Test User", "Test Subredit", 0, 0, "1 Hour Ago", false, false);
 
        Mockito.when(postRepository.findById(123L)).thenReturn(Optional.of(post));
        Mockito.when(postMapper.mapToDto(Mockito.any(Post.class))).thenReturn(expectedPostResponse);
 
        PostResponse actualPostResponse = postService.getPost(123L);
 
        Assertions.assertThat(actualPostResponse.getId()).isEqualTo(expectedPostResponse.getId());
        Assertions.assertThat(actualPostResponse.getPostName()).isEqualTo(expectedPostResponse.getPostName());
    }

    @Test
    @DisplayName("Should Save Posts")
    public void shouldSavePosts() {
        PostService postService = new PostService(postRepository, subredditRepository, userRepository, authService, postMapper);
    
        User currentUser = new User(123L, "test user", "secret password", "user@email.com", Instant.now(), true);
        Subreddit subreddit = new Subreddit(123L, "First Subreddit", "Subreddit Description", emptyList(), Instant.now(), currentUser);
        Post post = new Post(123L, "First Post", "http://url.site", "Test",
                0, null, Instant.now(), null);
        PostRequest postRequest = new PostRequest(null, "First Subreddit", "First Post", "http://url.site", "Test");
    
        Mockito.when(subredditRepository.findByName("First Subreddit"))
                .thenReturn(Optional.of(subreddit));
        Mockito.when(postMapper.map(postRequest, subreddit, currentUser))
                .thenReturn(post);
        postService.save(postRequest);
        Mockito.verify(postRepository, Mockito.times(1)).save(ArgumentMatchers.any(Post.class));    
    }
}
```

### Capturing Method Arguments

```java
@ExtendWith(MockitoExtension.class)
class PostServiceTest {
 
    @Mock
    private PostRepository postRepository;
    @Mock
    private SubredditRepository subredditRepository;
    @Mock
    private UserRepository userRepository;
    @Mock
    private AuthService authService;
    @Mock
    private PostMapper postMapper;
 
    @Captor
    private ArgumentCaptor<Post> postArgumentCaptor;
 
    @Test
    @DisplayName("Should Retrieve Post by Id")
    public void shouldFindPostById() {
 
        PostService postService = new PostService(postRepository, subredditRepository, userRepository, authService, postMapper);
 
        Post post = new Post(123L, "First Post", "http://url.site", "Test",
                0, null, Instant.now(), null);
        PostResponse expectedPostResponse = new PostResponse(123L, "First Post", "http://url.site", "Test",
                "Test User", "Test Subredit", 0, 0, "1 Hour Ago", false, false);
 
        Mockito.when(postRepository.findById(123L)).thenReturn(Optional.of(post));
        Mockito.when(postMapper.mapToDto(Mockito.any(Post.class))).thenReturn(expectedPostResponse);
 
        PostResponse actualPostResponse = postService.getPost(123L);
 
        Assertions.assertThat(actualPostResponse.getId()).isEqualTo(expectedPostResponse.getId());
        Assertions.assertThat(actualPostResponse.getPostName()).isEqualTo(expectedPostResponse.getPostName());
    }
 
    @Test
    @DisplayName("Should Save Posts")
    public void shouldSavePosts() {
        PostService postService = new PostService(postRepository, subredditRepository, userRepository, authService, postMapper);
 
        User currentUser = new User(123L, "test user", "secret password", "user@email.com", Instant.now(), true);
        Subreddit subreddit = new Subreddit(123L, "First Subreddit", "Subreddit Description", emptyList(), Instant.now(), currentUser);
        Post post = new Post(123L, "First Post", "http://url.site", "Test",
                0, null, Instant.now(), null);
        PostRequest postRequest = new PostRequest(null, "First Subreddit", "First Post", "http://url.site", "Test");
 
        Mockito.when(subredditRepository.findByName("First Subreddit"))
                .thenReturn(Optional.of(subreddit));
        Mockito.when(authService.getCurrentUser())
                .thenReturn(currentUser);
        Mockito.when(postMapper.map(postRequest, subreddit, currentUser))
                .thenReturn(post);
 
        postService.save(postRequest);
        Mockito.verify(postRepository, Mockito.times(1)).save(postArgumentCaptor.capture());
 
        Assertions.assertThat(postArgumentCaptor.getValue().getPostId()).isEqualTo(123L);
        Assertions.assertThat(postArgumentCaptor.getValue().getPostName()).isEqualTo("First Post");
    }
}
```
### Improving our Tests by using JUnit Lifecycle Methods
* ***@BeforeEach*** Using this annotation, we can define all the pre-processing logic required before running each test
* ***@AfterEach*** Using this annotation, we can define all the post-processing logic required after running each test.
* ***@BeforeAll*** Using this annotation, we can define all the pre-processing logic required before running the Test class. We will see how to see this annotation in the future parts.
* ***@AfterAll*** Using this annotation, we can define all the post-processing logic required after running the Test class. We will see how to see this annotation in the future parts.

```java
@ExtendWith(MockitoExtension.class)
class PostServiceTest {
 
    @Mock
    private PostRepository postRepository;
    @Mock
    private SubredditRepository subredditRepository;
    @Mock
    private UserRepository userRepository;
    @Mock
    private AuthService authService;
    @Mock
    private PostMapper postMapper; 
    @Captor
    private ArgumentCaptor<Post> postArgumentCaptor;
 
    private PostService postService;
 
    @BeforeEach
    public void setup() {
        postService = new PostService(postRepository, subredditRepository, userRepository, authService, postMapper);
    }
 
    @Test
    @DisplayName("Should Retrieve Post by Id")
    public void shouldFindPostById() {
        Post post = new Post(123L, "First Post", "http://url.site", "Test",
                0, null, Instant.now(), null);
        PostResponse expectedPostResponse = new PostResponse(123L, "First Post", "http://url.site", "Test",
                "Test User", "Test Subredit", 0, 0, "1 Hour Ago", false, false);
 
        Mockito.when(postRepository.findById(123L)).thenReturn(Optional.of(post));
        Mockito.when(postMapper.mapToDto(Mockito.any(Post.class))).thenReturn(expectedPostResponse);
 
        PostResponse actualPostResponse = postService.getPost(123L);
 
        Assertions.assertThat(actualPostResponse.getId()).isEqualTo(expectedPostResponse.getId());
        Assertions.assertThat(actualPostResponse.getPostName()).isEqualTo(expectedPostResponse.getPostName());
    }
 
    @Test
    @DisplayName("Should Save Posts")
    public void shouldSavePosts() {
        User currentUser = new User(123L, "test user", "secret password", "user@email.com", Instant.now(), true);
        Subreddit subreddit = new Subreddit(123L, "First Subreddit", "Subreddit Description", emptyList(), Instant.now(), currentUser);
        Post post = new Post(123L, "First Post", "http://url.site", "Test",
                0, null, Instant.now(), null);
        PostRequest postRequest = new PostRequest(null, "First Subreddit", "First Post", "http://url.site", "Test");
 
        Mockito.when(subredditRepository.findByName("First Subreddit"))
                .thenReturn(Optional.of(subreddit));
        Mockito.when(authService.getCurrentUser())
                .thenReturn(currentUser);
        Mockito.when(postMapper.map(postRequest, subreddit, currentUser))
                .thenReturn(post);
 
        postService.save(postRequest);
        Mockito.verify(postRepository, Mockito.times(1)).save(postArgumentCaptor.capture());
 
        Assertions.assertThat(postArgumentCaptor.getValue().getPostId()).isEqualTo(123L);
        Assertions.assertThat(postArgumentCaptor.getValue().getPostName()).isEqualTo("First Post");
    }
}
```

### Persistence Layer Test

```java
import com.programming.techie.springredditclone.BaseTest;
import com.programming.techie.springredditclone.model.Post;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.jdbc.AutoConfigureTestDatabase;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;

import java.time.Instant;

import static org.assertj.core.api.Assertions.assertThat;

@DataJpaTest
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
public class PostRepositoryTest {

    @Autowired
    private PostRepository postRepository;

    @Test
    public void shouldSavePost() {
        Post expectedPostObject = new Post(null, "First Post", "http://url.site", "Test",
                0, null, Instant.now(), null);
        Post actualPostObject = postRepository.save(expectedPostObject);

        assertThat(actualPostObject).usingRecursiveComparison()
                .ignoringFields("postId").isEqualTo(expectedPostObject);
    }

}
```

### Controller Layer Test

```java
import com.programming.techie.springredditclone.dto.PostResponse;
import com.programming.techie.springredditclone.security.JwtProvider;
import com.programming.techie.springredditclone.service.PostService;
import com.programming.techie.springredditclone.service.UserDetailsServiceImpl;
import org.hamcrest.Matchers;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;

import static java.util.Arrays.asList;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@WebMvcTest(controllers = PostController.class)
class PostControllerTest {

    @MockBean
    private PostService postService;
    @MockBean
    private UserDetailsServiceImpl userDetailsService;
    @MockBean
    private JwtProvider jwtProvider;

    @Autowired
    private MockMvc mockMvc;

    @Test
    @DisplayName("Should List All Posts When making GET request to endpoint - /api/posts/")
    void shouldCreatePost() throws Exception {
        PostResponse postRequest1 = new PostResponse(1L, "Post Name", "http://url.site", "Description", "User 1",
                "Subreddit Name", 0, 0, "1 day ago", false, false);
        PostResponse postRequest2 = new PostResponse(2L, "Post Name 2", "http://url2.site2", "Description2", "User 2",
                "Subreddit Name 2", 0, 0, "2 days ago", false, false);

        Mockito.when(postService.getAllPosts()).thenReturn(asList(postRequest1, postRequest2));

        mockMvc.perform(get("/api/posts/"))
                .andExpect(status().is(200))
                .andExpect(content().contentType(MediaType.APPLICATION_JSON_VALUE))
                .andExpect(jsonPath("$.size()", Matchers.is(2)))
                .andExpect(jsonPath("$[0].id", Matchers.is(1)))
                .andExpect(jsonPath("$[0].postName", Matchers.is("Post Name")))
                .andExpect(jsonPath("$[0].url", Matchers.is("http://url.site")))
                .andExpect(jsonPath("$[1].url", Matchers.is("http://url2.site2")))
                .andExpect(jsonPath("$[1].postName", Matchers.is("Post Name 2")))
                .andExpect(jsonPath("$[1].id", Matchers.is(2)));
    }
}
```

### Model Test

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.json.JsonTest;
import org.springframework.boot.test.json.JacksonTester;
import org.springframework.boot.test.json.JsonContent;
import org.springframework.test.context.junit.jupiter.SpringExtension;

import static org.assertj.core.api.Assertions.assertThat;

@ExtendWith(SpringExtension.class)
@JsonTest
class CreateUserRequestTests {

    @Autowired
    private JacksonTester<CreateUserRequest> jacksonTester;

    @Test
    void testSerialize() throws IOException {
        CreateUserRequest createUserRequest = new CreateUserRequest("ivan", "ivan@test", LocalDate.parse("2018-01-01"));

        JsonContent<CreateUserRequest> jsonContent = jacksonTester.write(createUserRequest);

        assertThat(jsonContent)
                .hasJsonPathStringValue("@.username")
                .extractingJsonPathStringValue("@.username").isEqualTo("ivan");

        assertThat(jsonContent)
                .hasJsonPathStringValue("@.email")
                .extractingJsonPathStringValue("@.email").isEqualTo("ivan@test");

        assertThat(jsonContent)
                .hasJsonPathStringValue("@.birthday")
                .extractingJsonPathStringValue("@.birthday").isEqualTo("2018-01-01");
    }

    @Test
    void testDeserialize() throws IOException {
        String content = "{\"username\":\"ivan\",\"email\":\"ivan@test\",\"birthday\":\"2018-01-01\"}";

        CreateUserRequest createUserRequest = jacksonTester.parseObject(content);

        assertThat(createUserRequest.getUsername()).isEqualTo("ivan");
        assertThat(createUserRequest.getEmail()).isEqualTo("ivan@test");
        assertThat(createUserRequest.getBirthday()).isEqualTo(LocalDate.parse("2018-01-01"));
    }
}
```