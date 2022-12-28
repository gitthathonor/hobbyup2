# :dart: hobbyup
온라인 취미 클래스 플랫폼 hobbyup
<br>

## :triangular_flag_on_post: 프로젝트 개요
<br>

### 레퍼런스 사이트(크몽)
![image](https://user-images.githubusercontent.com/95184357/209761704-869e35aa-3d01-41f5-a18c-d26fb38bdb5f.png)

'크몽'의 여러가지 서비스들 중에서 다양한 카테고리에 대한 전문성을 상품화하여 거래하는 서비스를 참조하였다.
<br>

### 개발 이유
1. 삶에서 여가의 중요성이 점점 증가하고 있다.
2. 단순히 클라이언트가 서버에서 데이터를 받는 것이 아니라, 클라이언트가 직접 다른 클라이언트에게 서비스를 제공하는 형태의 사이트를 구현하고 싶었다.
3. UI적인 측면에서 여러 사이트들을 둘러본 결과 '크몽'이 가장 마음에 들었다.
<br>

### 프롤로그
![image](https://user-images.githubusercontent.com/95184357/209767132-57089374-cb4e-4d9b-8011-18257704d31b.png)
<br>

### 테이블 구성
![image](https://user-images.githubusercontent.com/95184357/209767385-a37e2ea3-8898-4e1c-941c-4455ded5d9a5.png)
```sql
CREATE TABLE `users` (
	`id`	bigint	NOT NULL,
	`username`	varchar	NOT NULL,
	`password`	varchar	NOT NULL,
	`email`	varchar	NOT NULL,
	`phone_num`	varchar	NOT NULL,
	`created_at`	TimeStamp	NOT NULL,
	`updated_at`	TimeStamp	NOT NULL,
	`role`	varchar	NOT NULL	COMMENT 'default USER',
	`is_disabled`	boolean	NOT NULL	COMMENT 'default false'
);

CREATE TABLE `profile` (
	`id`	bigint	NOT NULL,
	`photo`	varchar	NOT NULL,
	`introduction`	longtext	NOT NULL,
	`region`	varchar	NOT NULL,
	`certification`	varchar	NOT NULL,
	`career_year`	varchar	NOT NULL,
	`career`	varchar	NOT NULL,
	`user_profile_id`	bigint	NOT NULL
);

CREATE TABLE `subscribe` (
	`id`	bigint	NOT NULL,
	`created_at`	TimeStamp	NOT NULL,
	`user_id`	bigint	NOT NULL,
	`lecture_id`	bigint	NOT NULL
);

CREATE TABLE `lesson` (
	`id`	bigint	NOT NULL,
	`name`	varchar	NOT NULL,
	`photo`	varchar	NOT NULL	COMMENT '파일은 하드나 클라우드에 저장,  DB에는 경로만 저장',
	`price`	bigint	NOT NULL,
	`curriculum`	longtext	NOT NULL,
	`lesson_time`	int	NOT NULL,
	`lesson_count`	int	NOT NULL,
	`possible_days`	varchar	NOT NULL	COMMENT ',로 파싱해서 response 해야한다.',
	`place`	varchar	NOT NULL	COMMENT 'PlaceEnum 만들어서 지정해줘야 됨',
	`policy`	longtext	NOT NULL,
	`expired_at`	TimeStamp	NOT NULL,
	`category_id`	bigint	NOT NULL,
	`expert_id`	bigint	NOT NULL
);

CREATE TABLE `coupon` (
	`id`	bigint	NOT NULL,
	`title`	varchar	NOT NULL,
	`price`	bigint	NOT NULL,
	`expired_date`	TimeStamp	NOT NULL,
	`created_at`	TimeStamp	NOT NULL,
	`user_coupon_id`	bigint	NOT NULL
);

CREATE TABLE `payment` (
	`id`	bigint	NOT NULL,
	`total_price`	bigint	NOT NULL,
	`total_count`	int	NOT NULL,
	`discount_price`	bigint	NOT NULL,
	`final_price`	bigint	NOT NULL,
	`created_at`	TimeStamp	NOT NULL,
	`user_id`	bigint	NOT NULL,
	`lecture_id`	bigint	NOT NULL,
	`payment_type_id`	bigint	NOT NULL
);

CREATE TABLE `review` (
	`id`	bigint	NOT NULL,
	`content`	longtext	NOT NULL,
	`grade`	double	NOT NULL,
	`lesson_id`	bigint	NOT NULL,
	`user_id`	bigint	NOT NULL
);

CREATE TABLE `payment_type` (
	`id`	bigint	NOT NULL,
	`type`	varchar	NOT NULL
);

CREATE TABLE `category` (
	`id`	bigint	NOT NULL,
	`name`	varchar	NOT NULL
);

CREATE TABLE `interest` (
	`id`	bigint	NOT NULL,
	`user_id`	bigint	NOT NULL,
	`category_id`	bigint	NOT NULL
);

CREATE TABLE `expert` (
	`id`	bigint	NOT NULL,
	`satisfication`	int	NOT NULL,
	`total_work`	int	NOT NULL,
	`is_approval`	boolean	NOT NULL	COMMENT 'true일 때, 서비스 판매 가능',
	`user_id`	bigint	NOT NULL
);

CREATE TABLE `claim` (
	`id`	bigint	NOT NULL,
	`expert_id`	bigint	NOT NULL
);

ALTER TABLE `users` ADD CONSTRAINT `PK_USERS` PRIMARY KEY (
	`id`
);

ALTER TABLE `profile` ADD CONSTRAINT `PK_PROFILE` PRIMARY KEY (
	`id`
);

ALTER TABLE `subscribe` ADD CONSTRAINT `PK_SUBSCRIBE` PRIMARY KEY (
	`id`
);

ALTER TABLE `lesson` ADD CONSTRAINT `PK_LESSON` PRIMARY KEY (
	`id`
);

ALTER TABLE `coupon` ADD CONSTRAINT `PK_COUPON` PRIMARY KEY (
	`id`
);

ALTER TABLE `payment` ADD CONSTRAINT `PK_PAYMENT` PRIMARY KEY (
	`id`
);

ALTER TABLE `review` ADD CONSTRAINT `PK_REVIEW` PRIMARY KEY (
	`id`
);

ALTER TABLE `payment_type` ADD CONSTRAINT `PK_PAYMENT_TYPE` PRIMARY KEY (
	`id`
);

ALTER TABLE `category` ADD CONSTRAINT `PK_CATEGORY` PRIMARY KEY (
	`id`
);

ALTER TABLE `interest` ADD CONSTRAINT `PK_INTEREST` PRIMARY KEY (
	`id`
);

ALTER TABLE `expert` ADD CONSTRAINT `PK_EXPERT` PRIMARY KEY (
	`id`
);

ALTER TABLE `claim` ADD CONSTRAINT `PK_CLAIM` PRIMARY KEY (
	`id`
);

```

