# Gin Web Framework

<img align="right" width="159px" src="https://raw.githubusercontent.com/gin-gonic/logo/master/color.png">

[![Build Status](https://github.com/PHPDevsr/gin-forked/actions/workflows/gin.yml/badge.svg?branch=develop)](https://github.com/PHPDevsr/gin-forked/actions/workflows/gin.yml)
[![codecov](https://codecov.io/gh/PHPDevsr/gin-forked/branch/master/graph/badge.svg)](https://codecov.io/gh/PHPDevsr/gin-forked)
[![Go Report Card](https://goreportcard.com/badge/github.com/PHPDevsr/gin-forked)](https://goreportcard.com/report/github.com/PHPDevsr/gin-forked)
[![Go Reference](https://pkg.go.dev/badge/github.com/PHPDevsr/gin-forked?status.svg)](https://pkg.go.dev/github.com/PHPDevsr/gin-forked?tab=doc)
[![Sourcegraph](https://sourcegraph.com/github.com/PHPDevsr/gin-forked/-/badge.svg)](https://sourcegraph.com/github.com/PHPDevsr/gin-forked?badge)
[![Open Source Helpers](https://www.codetriage.com/phpdevsr/gin-forked/badges/users.svg)](https://www.codetriage.com/PHPDevsr/gin-forked)
[![Release](https://img.shields.io/github/release/PHPDevsr/gin-forked.svg?style=flat-square)](https://github.com/PHPDevsr/gin-forked/releases)
[![TODOs](https://badgen.net/https/api.tickgit.com/badgen/github.com/PHPDevsr/gin-forked)](https://www.tickgit.com/browse?repo=github.com/PHPDevsr/gin-forked)

Gin is a web framework written in [Go](https://go.dev/). It features a martini-like API with performance that is up to 40 times faster thanks to [httprouter](https://github.com/julienschmidt/httprouter).
If you need performance and good productivity, you will love Gin.

**Gin's key features are:**

- **Zero allocation router** - Extremely memory-efficient routing with no heap allocations
- **High performance** - Benchmarks show superior speed compared to other Go web frameworks
- **Middleware support** - Extensible middleware system for authentication, logging, CORS, etc.
- **Crash-free** - Built-in recovery middleware prevents panics from crashing your server
- **JSON validation** - Automatic request/response JSON binding and validation
- **Route grouping** - Organize related routes and apply common middleware
- **Error management** - Centralized error handling and logging
- **Built-in rendering** - Support for JSON, XML, HTML templates, and more
- **Extensible** - Large ecosystem of community middleware and plugins

## Getting Started

### Prerequisites

- **Go version**: Gin requires [Go](https://go.dev/) version [1.24](https://go.dev/doc/devel/release#go1.24.0) or above
- **Basic Go knowledge**: Familiarity with Go syntax and package management is helpful

### Installation

With [Go's module support](https://go.dev/wiki/Modules#how-to-use-modules), simply import Gin in your code and Go will automatically fetch it during build:

```sh
import "github.com/PHPDevsr/gin-forked"
```

Alternatively, use `go get`:

```sh
go get -u github.com/PHPDevsr/gin-forked
```

### Running Gin

A basic example:

```go
package main

import (
  "net/http"

  "github.com/PHPDevsr/gin-forked"
)

func main() {
  // Create a Gin router with default middleware (logger and recovery)
  r := gin.Default()
  
  // Define a simple GET endpoint
  r.GET("/ping", func(c *gin.Context) {
    // Return JSON response
    c.JSON(http.StatusOK, gin.H{
      "message": "pong",
    })
  })
  
  // Start server on port 8080 (default)
  // Server will listen on 0.0.0.0:8080 (localhost:8080 on Windows)
  r.Run()
}
```

**Running the application:**

1. Save the code above as `main.go`
2. Run the application:

   ```sh
   go run main.go
   ```

3. Open your browser and visit [`http://localhost:8080/ping`](http://localhost:8080/ping)
4. You should see: `{"message":"pong"}`

**What this example demonstrates:**

- Creating a Gin router with default middleware
- Defining HTTP endpoints with simple handler functions
- Returning JSON responses
- Starting an HTTP server

### Next Steps

After running your first Gin application, explore these resources to learn more:

#### 📚 Learning Resources

- **[Gin Quick Start Guide](docs/doc.md)** - Comprehensive tutorial with API examples and build configurations
- **[Example Repository](https://github.com/gin-gonic/examples)** - Ready-to-run examples demonstrating various Gin use cases:
  - REST API development
  - Authentication & middleware
  - File uploads and downloads
  - WebSocket connections
  - Template rendering

## 📖 Documentation

### API Reference

- **[Go.dev API Documentation](https://pkg.go.dev/github.com/gin-gonic/gin)** - Complete API reference with examples

### User Guides

The comprehensive documentation is available on [gin-gonic.com](https://gin-gonic.com) in multiple languages:

- [English](https://gin-gonic.com/en/docs/) | [简体中文](https://gin-gonic.com/zh-cn/docs/) | [繁體中文](https://gin-gonic.com/zh-tw/docs/)
- [日本語](https://gin-gonic.com/ja/docs/) | [한국어](https://gin-gonic.com/ko-kr/docs/) | [Español](https://gin-gonic.com/es/docs/)
- [Turkish](https://gin-gonic.com/tr/docs/) | [Persian](https://gin-gonic.com/fa/docs/) | [Português](https://gin-gonic.com/pt/docs/)
- [Russian](https://gin-gonic.com/ru/docs/) | [Indonesian](https://gin-gonic.com/id/docs/)

### Official Tutorials

- [Go.dev Tutorial: Developing a RESTful API with Go and Gin](https://go.dev/doc/tutorial/web-service-gin)

## ⚡ Performance Benchmarks

Gin demonstrates exceptional performance compared to other Go web frameworks. It uses a custom version of [HttpRouter](https://github.com/julienschmidt/httprouter) for maximum efficiency. [View detailed benchmarks →](/BENCHMARKS.md)

**Gin vs. Other Go Frameworks** (GitHub API routing benchmark):

| Benchmark name                 |       (1) |             (2) |          (3) |             (4) |
| ------------------------------ | --------: | --------------: | -----------: | --------------: |
| BenchmarkGin_GithubAll         | **43550** | **27364 ns/op** |   **0 B/op** | **0 allocs/op** |
| BenchmarkAce_GithubAll         |     40543 |     29670 ns/op |       0 B/op |     0 allocs/op |
| BenchmarkAero_GithubAll        |     57632 |     20648 ns/op |       0 B/op |     0 allocs/op |
| BenchmarkBear_GithubAll        |      9234 |    216179 ns/op |   86448 B/op |   943 allocs/op |
| BenchmarkBeego_GithubAll       |      7407 |    243496 ns/op |   71456 B/op |   609 allocs/op |
| BenchmarkBone_GithubAll        |       420 |   2922835 ns/op |  720160 B/op |  8620 allocs/op |
| BenchmarkChi_GithubAll         |      7620 |    238331 ns/op |   87696 B/op |   609 allocs/op |
| BenchmarkDenco_GithubAll       |     18355 |     64494 ns/op |   20224 B/op |   167 allocs/op |
| BenchmarkEcho_GithubAll        |     31251 |     38479 ns/op |       0 B/op |     0 allocs/op |
| BenchmarkGocraftWeb_GithubAll  |      4117 |    300062 ns/op |  131656 B/op |  1686 allocs/op |
| BenchmarkGoji_GithubAll        |      3274 |    416158 ns/op |   56112 B/op |   334 allocs/op |
| BenchmarkGojiv2_GithubAll      |      1402 |    870518 ns/op |  352720 B/op |  4321 allocs/op |
| BenchmarkGoJsonRest_GithubAll  |      2976 |    401507 ns/op |  134371 B/op |  2737 allocs/op |
| BenchmarkGoRestful_GithubAll   |       410 |   2913158 ns/op |  910144 B/op |  2938 allocs/op |
| BenchmarkGorillaMux_GithubAll  |       346 |   3384987 ns/op |  251650 B/op |  1994 allocs/op |
| BenchmarkGowwwRouter_GithubAll |     10000 |    143025 ns/op |   72144 B/op |   501 allocs/op |
| BenchmarkHttpRouter_GithubAll  |     55938 |     21360 ns/op |       0 B/op |     0 allocs/op |
| BenchmarkHttpTreeMux_GithubAll |     10000 |    153944 ns/op |   65856 B/op |   671 allocs/op |
| BenchmarkKocha_GithubAll       |     10000 |    106315 ns/op |   23304 B/op |   843 allocs/op |
| BenchmarkLARS_GithubAll        |     47779 |     25084 ns/op |       0 B/op |     0 allocs/op |
| BenchmarkMacaron_GithubAll     |      3266 |    371907 ns/op |  149409 B/op |  1624 allocs/op |
| BenchmarkMartini_GithubAll     |       331 |   3444706 ns/op |  226551 B/op |  2325 allocs/op |
| BenchmarkPat_GithubAll         |       273 |   4381818 ns/op | 1483152 B/op | 26963 allocs/op |
| BenchmarkPossum_GithubAll      |     10000 |    164367 ns/op |   84448 B/op |   609 allocs/op |
| BenchmarkR2router_GithubAll    |     10000 |    160220 ns/op |   77328 B/op |   979 allocs/op |
| BenchmarkRivet_GithubAll       |     14625 |     82453 ns/op |   16272 B/op |   167 allocs/op |
| BenchmarkTango_GithubAll       |      6255 |    279611 ns/op |   63826 B/op |  1618 allocs/op |
| BenchmarkTigerTonic_GithubAll  |      2008 |    687874 ns/op |  193856 B/op |  4474 allocs/op |
| BenchmarkTraffic_GithubAll     |       355 |   3478508 ns/op |  820744 B/op | 14114 allocs/op |
| BenchmarkVulcan_GithubAll      |      6885 |    193333 ns/op |   19894 B/op |   609 allocs/op |

- (1): Total Repetitions achieved in constant time, higher means more confident result
- (2): Single Repetition Duration (ns/op), lower is better
- (3): Heap Memory (B/op), lower is better
- (4): Average Allocations per Repetition (allocs/op), lower is better

## Middleware

You can find many useful Gin middlewares at [gin-contrib](https://github.com/gin-contrib) and [gin-gonic/contrib](https://github.com/gin-gonic/contrib).

## Uses

Here are some awesome projects that are using the [Gin](https://github.com/PHPDevsr/gin-forked) web framework.

- **[gorush](https://github.com/appleboy/gorush)** - High-performance push notification server
- **[fnproject](https://github.com/fnproject/fn)** - Container-native, serverless platform
- **[photoprism](https://github.com/photoprism/photoprism)** - AI-powered personal photo management
- **[lura](https://github.com/luraproject/lura)** - Ultra-performant API Gateway framework
- **[picfit](https://github.com/thoas/picfit)** - Real-time image processing server
- **[dkron](https://github.com/distribworks/dkron)** - Distributed job scheduling system

## 🤝 Contributing

Gin is the work of hundreds of contributors from around the world. We welcome and appreciate your contributions!

### How to Contribute

- 🐛 **Report bugs** - Help us identify and fix issues
- 💡 **Suggest features** - Share your ideas for improvements
- 📝 **Improve documentation** - Help make our docs clearer
- 🔧 **Submit code** - Fix bugs or implement new features
- 🧪 **Write tests** - Improve our test coverage

### Getting Started with Contributing

1. Check out our [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines
2. Join our community discussions and ask questions

**All contributions are valued and help make Gin better for everyone!**
