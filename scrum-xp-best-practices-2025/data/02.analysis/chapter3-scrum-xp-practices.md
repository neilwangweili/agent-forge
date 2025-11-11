# 第三章：Scrum + XP 最佳实践流程

## 3.1 整体流程概览

Scrum提供了项目管理的框架，XP提供了工程实践的方法。两者结合，形成了从需求到部署的完整敏捷开发方法论。Scrum解决"做什么"和"何时做"的问题，XP解决"怎么做"和"如何保证质量"的问题。

完整的Scrum + XP实践流程包括五个主要阶段：

```
需求分析 → Sprint计划 → 编码实践 → 质量保障 → 交付部署
   ↓          ↓           ↓          ↓           ↓
领域建模   编写用户     TDD驱动    端到端测试   自动化部署
用户故事   故事和AC     结对编程   验收测试     监控反馈
  地图                  持续集成    CI/CD
```

这个流程是迭代的，每个Sprint都会重复。每个Sprint的输出是一个可工作的增量，经过完整的测试和验证，可以部署到生产环境。

## 3.2 第一步：领域建模 + 用户故事地图

在Sprint Planning之前或项目初期，团队需要建立对业务领域的共同理解。领域建模和用户故事地图是两个互补的技术，前者聚焦于业务概念和规则，后者聚焦于用户旅程和功能优先级。

### 领域建模

领域建模识别业务领域的核心概念、实体、关系和规则。Event Storming是一种有效的协作式领域建模技术。团队和领域专家聚集在一起，在墙上贴便利贴：橙色便利贴表示领域事件（如"订单已创建"、"支付已完成"），蓝色表示命令（触发事件的操作），黄色表示聚合（负责处理命令和产生事件的领域对象）。

通过Event Storming，团队可以识别：
- **实体（Entity）**：有唯一标识的领域对象，如User、Order、Product
- **值对象（Value Object）**：通过属性值区分的对象，如Email、Address、Money
- **聚合（Aggregate）**：一组相关实体和值对象的集合，有聚合根维护一致性
- **边界上下文（Bounded Context）**：不同的业务子域，有清晰的边界和独立的模型
- **通用语言（Ubiquitous Language）**：团队共享的业务术语，代码中使用相同的术语

领域模型不是一次性完成的，而是随着团队对业务的理解逐步演进的。初期的模型可能较粗糙，随着开发的进行，模型会越来越精确。

### 用户故事地图

用户故事地图由Jeff Patton提出，通过可视化用户旅程来识别和组织用户故事。故事地图有两个维度：

**横向（用户旅程）**：从左到右展示用户使用产品的时间顺序。顶部是用户活动（User Activities），高层次的用户目标，如"浏览商品"、"下单购买"、"管理订单"。

**纵向（优先级）**：从上到下展示故事的优先级和细节。最上方是骨架（Backbone），用户活动。往下是用户故事，按价值和风险排序。最上面的是MVP（Minimum Viable Product），第一个可交付的最小功能集。

Story Mapping使团队能够：
- 可视化产品全貌，避免只见树木不见森林
- 从用户视角组织需求，确保用户价值
- 清晰地识别MVP和后续版本的范围
- 促进团队协作，所有人围绕地图讨论
- 识别遗漏的功能，发现用户旅程中的空白

Story Mapping与领域建模的结合：从Story Map中提取的用户故事可以帮助识别领域概念。例如，"用户下单"的故事涉及Order、Product、Payment等领域概念。领域模型反过来帮助细化和验证用户故事，确保故事在业务上是合理的。

## 3.3 第二步：编写用户故事和验收标准

在Sprint Planning中，Product Owner和团队共同将Product Backlog中的项细化为用户故事。每个用户故事遵循标准格式：

**As a [角色], I want [功能], So that [价值]**

例如：
- As a customer, I want to search products by category, So that I can quickly find what I need
- As an admin, I want to view sales reports, So that I can make informed business decisions

用户故事应该遵循INVEST原则：
- **Independent（独立）**：故事之间尽量独立，可以以任意顺序实现
- **Negotiable（可协商）**：故事是对话的承诺，细节可协商
- **Valuable（有价值）**：每个故事都为用户提供价值
- **Estimable（可估算）**：团队能够估算故事的大小
- **Small（小）**：故事应该足够小，可以在一个Sprint内完成
- **Testable（可测试）**：故事有明确的验收标准

验收标准（Acceptance Criteria, AC）定义了故事完成的定义。AC通常采用Given-When-Then格式（BDD风格）：

```
Given I am on the product search page
When I select "Electronics" category and click "Search"
Then I should see all products in the Electronics category
And the products should be sorted by relevance
And I should see product name, price, and image for each product
```

AC是故事和测试之间的桥梁。每个AC应该对应一个或多个自动化测试。清晰的AC使开发者知道要实现什么，测试者知道要验证什么，Product Owner知道如何接受故事。

## 3.4 第三步：TDD驱动的编码实践

从验收标准到可工作的代码，遵循从外到内、从测试到实现的路径。

### 从AC到测试用例

每个AC应该转化为一个或多个自动化测试。测试金字塔指导测试的分布：

**端到端测试（E2E Tests）**位于金字塔顶端，数量最少但覆盖关键用户场景。E2E测试模拟真实用户操作，验证完整的用户流程。例如，对于"搜索产品"的AC，E2E测试会：打开浏览器 → 导航到搜索页 → 选择分类 → 点击搜索 → 验证结果。E2E测试使用Selenium、Cypress、Playwright等工具。

**集成测试（Integration Tests）**位于金字塔中层，测试多个组件之间的交互。例如，测试搜索服务与数据库的交互，验证查询是否正确返回结果。集成测试可能使用TestContainers启动真实的数据库容器，或使用测试数据库。

**单元测试（Unit Tests）**位于金字塔底层，数量最多。单元测试测试单个函数、方法或类的行为。例如，测试产品过滤逻辑、排序逻辑、价格格式化等。单元测试快速、隔离、可重复，是TDD的核心。

### TDD红-绿-重构循环

对于每个功能，遵循TDD循环：

1. **红**：写一个失败的单元测试。测试描述了期望的行为。例如，测试ProductService的search方法应该返回指定分类的产品。运行测试，测试失败（红色）。

2. **绿**：写最少的代码让测试通过。实现ProductService的search方法，查询数据库，返回结果。运行测试，测试通过（绿色）。

3. **重构**：改进代码质量。消除重复，改善命名，提取方法。运行测试，确保仍然通过。

重复这个循环，逐步构建功能。每个循环都很小，可能只需要几分钟。小步前进降低了认知负担，使开发者可以专注于一个小目标。

### Smart Domain模式与小对象模式的应用

在实现领域逻辑时，应用Smart Domain模式和小对象模式提升代码质量。

**避免贫血模型**：贫血模型是指领域对象只有getter/setter，没有业务逻辑。业务逻辑分散在服务层，导致重复和不一致。

贫血模型示例：
```java
public class Order {
    private String id;
    private BigDecimal amount;
    private String status;
    // getters and setters
}

public class OrderService {
    public void approveOrder(Order order) {
        if (order.getAmount().compareTo(BigDecimal.ZERO) <= 0) {
            throw new IllegalArgumentException("Invalid amount");
        }
        if (!"PENDING".equals(order.getStatus())) {
            throw new IllegalStateException("Order not pending");
        }
        order.setStatus("APPROVED");
    }
}
```

问题：验证逻辑在服务层，容易重复。Order对象是被动的数据容器，不负责维护自己的一致性。

**采用富领域模型**：将业务逻辑封装在领域对象中，对象负责维护不变性。

富领域模型示例：
```java
public class Order {
    private final OrderId id;
    private final Money amount;
    private OrderStatus status;

    public Order(OrderId id, Money amount) {
        this.id = id;
        this.amount = amount;
        this.status = OrderStatus.PENDING;
    }

    public void approve() {
        if (!status.canTransitionTo(OrderStatus.APPROVED)) {
            throw new IllegalStateException("Cannot approve order in status: " + status);
        }
        this.status = OrderStatus.APPROVED;
    }
}

public class OrderService {
    public void approveOrder(Order order) {
        order.approve(); // 业务逻辑在Order中
    }
}
```

优势：业务规则集中在Order中，避免重复。Order负责维护自己的一致性，服务层只需调用领域对象的方法。

**使用Value Objects拒绝原始类型偏执**：原始类型偏执是指过度使用String、int等原始类型，而非创建有意义的小对象。

原始类型偏执示例：
```java
public class User {
    private String email;
    private String name;

    public User(String email, String name) {
        if (!email.contains("@")) {
            throw new IllegalArgumentException("Invalid email");
        }
        this.email = email;
        this.name = name;
    }

    public void sendEmail(String email, String message) { ... }
}
```

问题：email和name都是String，容易传错。验证逻辑分散在多处。

使用Value Objects：
```java
public class Email {
    private final String value;

    public Email(String value) {
        if (!isValid(value)) {
            throw new IllegalArgumentException("Invalid email: " + value);
        }
        this.value = value;
    }

    private static boolean isValid(String email) {
        return email.matches("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$");
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Email email = (Email) o;
        return value.equals(email.value);
    }

    @Override
    public int hashCode() {
        return value.hashCode();
    }
}

public class User {
    private final Email email;
    private final String name;

    public User(Email email, String name) {
        this.email = email;
        this.name = name;
    }

    public void sendEmail(Email recipient, String message) { ... }
}
```

优势：类型安全（不能将email传递给name参数），验证集中（只在Email构造函数），业务语义清晰（看到Email就知道是邮箱），易于重构（修改email格式只需修改Email类）。

其他Value Objects示例：
- **Money**：封装金额和货币，提供货币转换和算术运算
- **ZipCode**：验证邮编格式
- **PhoneNumber**：验证电话号码格式
- **URL**：解析和验证URL，提供协议、域名、路径等属性

### Pair Programming和Collective Code Ownership

在编码过程中，采用Pair Programming促进知识共享和提升代码质量。两人结对时，驾驶员专注于编写代码，导航员思考整体设计、边界情况、下一步方向。定期切换角色，通常每15-30分钟。

Collective Code Ownership意味着任何团队成员都可以修改任何代码。没有代码归属权，没有"我的模块"或"你的模块"。通过Pair Programming和代码审查，知识在团队中传播，避免知识孤岛。

## 3.5 第四步：端到端测试与验收测试

当所有单元测试和集成测试通过后，运行端到端测试和验收测试，验证完整的用户场景。

### 端到端测试

端到端测试模拟真实用户操作，验证完整流程。例如，对于"搜索产品"的用户故事，E2E测试会：
1. 启动应用（可能是本地部署或测试环境）
2. 打开浏览器，导航到搜索页
3. 选择分类"Electronics"
4. 点击"Search"按钮
5. 验证结果：显示电子产品，按相关性排序，每个产品显示名称、价格、图片

E2E测试使用Cypress、Playwright等工具。测试代码可能如下：
```javascript
test('search products by category', async () => {
    await page.goto('/search');
    await page.selectOption('#category', 'Electronics');
    await page.click('#search-button');

    const products = await page.$$('.product-item');
    expect(products.length).toBeGreaterThan(0);

    const firstProduct = products[0];
    expect(await firstProduct.$('.product-name')).toBeTruthy();
    expect(await firstProduct.$('.product-price')).toBeTruthy();
    expect(await firstProduct.$('.product-image')).toBeTruthy();
});
```

E2E测试较慢（可能需要几秒到几分钟），数量应该控制在5-10%。只测试关键的用户流程，不测试所有边界情况（边界情况由单元测试覆盖）。

### 验收测试

验收测试与AC一一对应，验证故事是否满足验收标准。验收测试可以是自动化的（如BDD测试），也可以是手动的（如探索性测试）。

BDD（Behavior-Driven Development）使用Given-When-Then格式编写测试，可以使用Cucumber、SpecFlow等工具。测试用自然语言描述，业务人员可读：

```gherkin
Feature: Product Search

Scenario: Search products by category
    Given I am on the product search page
    When I select "Electronics" category
    And I click "Search" button
    Then I should see products in "Electronics" category
    And products should be sorted by relevance
    And each product should show name, price, and image
```

这些自然语言的测试步骤对应到代码实现，执行实际的测试逻辑。

### CI/CD集成

每次代码提交到主线，CI服务器自动触发构建和测试流程：
1. **编译代码**：确保代码可以编译
2. **运行单元测试**：快速反馈（几秒到几分钟）
3. **运行集成测试**：验证模块间协作（几分钟）
4. **运行E2E测试**：验证完整流程（几分钟到几十分钟）
5. **静态代码分析**：检查代码质量、安全漏洞（SonarQube）
6. **生成报告**：测试覆盖率、代码质量指标

如果任何步骤失败，构建失败，团队立即收到通知。修复失败的构建是最高优先级。

Martin Fowler强调，构建应该在10分钟内完成（至少是快速的反馈阶段）。如果E2E测试较慢，可以分成快速反馈阶段（单元和集成测试，10分钟内）和完整验证阶段（包含E2E测试，可能需要更长时间）。

## 3.6 第五步：自动化部署

当所有测试通过，代码可以部署到生产环境。持续交付管道自动化了这个过程。

### 部署管道

部署管道包括多个阶段：
1. **Commit阶段**：编译、单元测试、静态分析（5-10分钟）
2. **Acceptance阶段**：集成测试、E2E测试（30-60分钟）
3. **Performance阶段**：性能测试、负载测试（几小时，可选）
4. **Production阶段**：部署到生产环境

每个阶段通过后，产物（artifact）晋升到下一阶段。只构建一次二进制文件，在各环境间传递，确保部署到生产的正是经过测试的版本。

### 部署策略

**蓝绿部署（Blue-Green Deployment）**：维护两个生产环境，蓝色是当前版本，绿色是新版本。部署到绿色环境，测试通过后切换流量到绿色。如果出现问题，立即切回蓝色。优势是零停机、快速回滚，劣势是需要双倍资源。

**金丝雀部署（Canary Deployment）**：先部署到小部分用户（如5%），监控指标（错误率、响应时间、业务指标）。如果正常，逐步扩大范围（10%、25%、50%、100%）。如果出现问题，立即回滚。优势是降低风险、早期发现问题，劣势是需要复杂的路由和监控。

**Feature Flags**：代码部署与功能发布解耦。新功能代码已部署但通过配置开关控制是否启用。可以为不同用户群体启用不同功能，A/B测试，快速回滚（关闭开关即可）。

### 监控与反馈

部署后，通过监控快速发现问题：
- **日志（Logs）**：记录应用行为，调试问题
- **指标（Metrics）**：响应时间、吞吐量、错误率、CPU/内存使用率
- **告警（Alerts）**：异常时自动通知团队
- **分布式追踪（Distributed Tracing）**：在微服务架构中追踪请求跨服务的路径

监控数据反馈到下一个Sprint的规划，形成闭环。性能问题、用户反馈、错误日志都成为Product Backlog的输入。

## 3.7 完整流程示例

以"用户搜索产品"功能为例，展示完整流程：

1. **领域建模**：识别Product、Category、SearchService等领域概念

2. **用户故事地图**：在"浏览商品"用户活动下，添加"搜索产品"故事

3. **编写用户故事**：As a customer, I want to search products by category, So that I can quickly find what I need

4. **编写AC**：
   - Given用户在搜索页，When选择分类并搜索，Then显示该分类的产品
   - 产品按相关性排序
   - 每个产品显示名称、价格、图片

5. **编写E2E测试**（红）：测试完整的搜索流程，测试失败

6. **编写集成测试**（红）：测试SearchService与数据库的交互，测试失败

7. **编写单元测试**（红）：测试产品过滤逻辑，测试失败

8. **实现功能**（绿）：
   - 实现SearchService的search方法
   - 使用Product（富领域模型）和Category（Value Object）
   - 运行单元测试，通过

9. **重构**：改进命名，提取方法，运行测试，仍然通过

10. **运行集成测试和E2E测试**：全部通过

11. **提交代码**：触发CI，构建和测试自动运行

12. **部署**：通过CD管道部署到测试环境，然后生产环境

13. **监控**：观察指标，确认功能正常

14. **Sprint Review**：演示功能，收集反馈

15. **Sprint Retrospective**：团队反思流程，识别改进机会

## 总结

Scrum + XP提供了完整的敏捷开发方法论。Scrum的迭代框架（Sprint Planning、Daily Scrum、Sprint Review、Retrospective）提供了节奏和反馈机制。XP的工程实践（TDD、Pair Programming、CI、简单设计）确保了代码质量。领域建模和用户故事地图连接业务需求与技术实现。Smart Domain和Value Objects提升代码的类型安全性和可维护性。CI/CD实现了从代码到生产的自动化流程。

这不是理论，而是经过大量实践验证的方法。Danske Bank、Akbank、British Telecom等组织的成功案例证明了这套方法的价值。Standish Group的数据显示，敏捷项目成功率是瀑布的3倍。Microsoft和IBM的研究证明，TDD降低缺陷率40-80%。这些数据共同支持了一个结论：Scrum + XP是现代软件开发的最佳实践。
