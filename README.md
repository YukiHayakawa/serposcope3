# serposcope

## 環境変数を変更

```
$ mv .env.sample .env
```

## ローカル

### 直接 Dockerfile をビルド

```
$ export $(cat .env | xargs) && docker build --build-arg SERPOSCOPE_VERSION=$SERPOSCOPE_VERSION --build-arg CPU_MODEL=$CPU_MODEL -t serposcope ./serposcope/
```

### ビルド

```
$ docker-compose -f docker-compose.local.yml build
```

### 起動

```
$ docker-compose -f docker-compose.local.yml up -d
```

### 停止

```
$ docker-compose down
```

## 本番等

### ビルド

```
$ docker-compose build
```

### 起動

```
$ docker-compose up -d
```

### 停止

```
$ docker-compose down
```
